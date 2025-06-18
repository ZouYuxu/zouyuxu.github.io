### 主要代码

```java
package com.wistron.sdbcontext.ohs.local.handler.util.syncdb;

import org.apache.camel.builder.RouteBuilder;
import org.apache.camel.processor.aggregate.GroupedBodyAggregationStrategy;
import org.springframework.stereotype.Component;

import java.util.List;

@Component
public class ApiTriggeredSyncRoute extends RouteBuilder {

    @Override
    public void configure() {
        // 定义REST端点
        rest()
                .description("数据库表同步服务")
                .post("/sync")
                .description("触发表同步作业")
                .routeId("api-triggered-sync")
                // 调用同步逻辑
                .to("direct:performSync")// 添加响应处理
                // 添加响应处理
                .responseMessage(200, "OK");

        // 实际的同步逻辑
        from("direct:performSync")
                .routeId("performSyncRoute")
                .to("sql:SELECT * FROM pcp.whq_pcp_hcm_employeeinfo where batch_id=(select max(batch_id) from pcp.whq_pcp_hcm_employeeinfo)?dataSource=#dataZoneDataSource")
                .process(exchange -> {
                    log.info("Body type: " + exchange.getIn().getBody().getClass());
                    log.info("First row keys: " + ((List<?>) exchange.getIn().getBody()).get(0));
                })
                .to("sql:DELETE FROM dzinbound.whq_hr_hcm_employeeinfo_bk?dataSource=#postgresqlDataSource")
                .log("目标表已清空")
//                .split(body())
//                .aggregate(constant(true), new GroupedBodyAggregationStrategy())
//                .completionSize(2000) // 每2000条批处理
//                .completionTimeout(300000) // 设置超时时间为5分钟
                // 临时修改为只插入前3个字段测试
//                .to("sql:INSERT INTO dzinbound.whq_hr_hcm_employeeinfo_bk(pkid, batchid, bu) " +
//                        "VALUES(:#pkid, :#batchid, :#bu)?dataSource=#postgresqlDataSource")
                .to("sql:INSERT INTO dzinbound.whq_hr_hcm_employeeinfo_bk VALUES (:#pkid,:#batchid,:#bu,:#bg,:#site,:#plant,:#location,:#emplid,:#name,:#name_a,:#hire_dt,:#sal_location_a,:#company,:#deptid,:#jobtitle_descr,:#emailid,:#email_address_a,:#phone_a,:#officer_level_a,:#supervisor_id,:#tree_level_num,:#termination_dt,:#labor_type,:#job_family,:#last_updt_dt,:#jobcode,:#desk_location,:#per_org,:#full_part_time,:#pay_group,:#labor_type_descr,:#cmpny_seniority_dt,:#supv_lvl_id,:#tree_level,:#sal_location,:#last_hire_dt,:#batch_id,:#version_id)?dataSource=#postgresqlDataSource&batch=true")
                .log("数据同步完成")
                .end();
    }
}
```

### 添加依赖

```xml
        <!-- 基础依赖 -->
        <dependency>
            <groupId>org.apache.camel.springboot</groupId>
            <artifactId>camel-spring-boot-starter</artifactId>
            <version>4.10.2</version>
        </dependency>

        <dependency>
            <groupId>org.apache.camel.springboot</groupId>
            <artifactId>camel-servlet-starter</artifactId>
            <version>4.10.2</version>
        </dependency>

        <!-- Camel SQL 组件 -->
        <dependency>
            <groupId>org.apache.camel.springboot</groupId>
            <artifactId>camel-sql-starter</artifactId>
            <version>4.10.2</version>
        </dependency>
        <dependency>
            <groupId>org.apache.camel.springboot</groupId>
            <artifactId>camel-rest-starter</artifactId>
            <version>4.10.2</version>
            <!-- use the same version as your Camel core version -->
        </dependency>
```

### 使用细节

直接post camel/sync即可
