### debounce防抖

调用方法inputvalue

```ts
(inputValue)="getVendorListDebouncedFunc($event)"

<input nz-input [(ngModel)]="item.value" [maxlength]="item?.maxChars ? item.maxChars:100"
            (input)="inputValueChange($event, item)" placeholder="{{item.placeholder}}" [nzAutocomplete]="auto"
            [disabled]="item.disabled" />
```

导入和编写

```ts
import { debounce, DebouncedFunc } from 'lodash';

getVendorListDebouncedFunc: DebouncedFunc<(value: any) => void>;

constructor(
    this.getVendorListDebouncedFunc = debounce(
      this.getVendorList.bind(this),
      300
    );
  }

getVendorList(param) {
    const { identify, inputValue } = param;
    this.callApiCommonService
}

```

如何使用angular进行测试

如何不断测试，修改文件即进行测试

Jasmine中的关键词

### fit

只测试这个测试用例

### xit

排除这个测试用例

### pending

测试用例内部动态的取消后续代码

java.sql.SQLTransientConnectionException: HikariPool-1 - Connection is not available, request timed out after 30000ms."}

2024-09-06 09:26:46

{"time":"2024-09-06T01:26:46.634353538Z","stream":"stdout","logtag":"F","message":"2024-09-06 09:26:46.633 \u001B[1;31mERROR\u001B[0;39m --- [nio-8089-exec-1] \u001B[36mc.w.s.o.l.h.u.GlobalExceptionHandlerUtil\u001B[0;39m : exception occurs:Could not open JDBC Connection for transaction，Exception types：class org.springframework.transaction.CannotCreateTransactionException, cause : {}"}

db连线超时，~~是因为使用的是jdbc:postgresql://10.20.100.4:6432/psc?useUnicode=true&characterEncoding=utf-8&prepareThreshold=0~~

是因为这段代码导致了call这个api的时候，会导致所有的连线超时，需要重启

可能是连线数超过了吧
[feature:customer:maintain (!51) · Merge requests · Avatar / avtsdm / command / avtsdm_sdbapi · GitLab (wistron.com)](https://gitlab.wistron.com/avatar/avtsdm/command/avtsdm_sdbapi/-/merge_requests/51/diffs)

```java

        Connection connection = dataSource.getConnection();
        additionalPicList = initParamList(additionalPicList);
        Array additionalPicArray = connection.createArrayOf("text", additionalPicList.toArray(new String[0]));
```

### 删除bypassSecurityTrustHtml

这个方法会导致sonarqube hotspot
