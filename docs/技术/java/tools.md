### BeanUtils

同时两个注解的问题，就用hasOneOf

```java

        JacksonAnnotationIntrospectordynamicIgnoreJacksonAnnotationIntrospector = newJacksonAnnotationIntrospector() {

            @Override

            publicbooleanhasIgnoreMarker(AnnotatedMemberm) {

                // 同时保留原生 @MyJsonIgnore 的功能

                returnsuper.hasIgnoreMarker(m)

                        || m.hasAnnotation(JsonIgnore.class)

                        || m.hasAnnotation(MyJsonIgnore.class)

                        || m.hasAnnotation(DynamicIgnore.class)

                        || m.hasOneOf(newClass[]{DynamicIgnore.class, JsonFormat.class});

            }

        };


        dynamicIgnoreMapper = newObjectMapper();

        dynamicIgnoreMapper.setAnnotationIntrospector(dynamicIgnoreJacksonAnnotationIntrospector);

```

#### Convert对象转为Long

第二个参数可以传默认值，不传默认null

如果null的情况的话，要特殊处理

```java

Longid = Convert.toLong(fieldValue);


```

#### CopyOptions

```java

// 修改后的代码片段

            CopyOptionscopyOptions = CopyOptions.create()

                // 添加注解过滤条件

                .setPropertiesFilter((srcProp, targetProp) -> {

                    try {

                        // 获取目标对象的字段对象

                        FieldtargetField = brandSurveyDocumentVo.getClass().getDeclaredField(targetProp.getFieldName());

                        // 检查是否存在@JsonIgnore注解

                        return !targetField.isAnnotationPresent(JsonIgnore.class);

                    } catch (NoSuchFieldExceptione) {

                        // 字段不存在时保留原始逻辑

                        returntrue;

                    }

                });

```

```java

CopyOptions.create()

                .setPropertiesFilter((filed, destField) -> {

                    filed.setAccessible(true);

                    return !filed.isAnnotationPresent(JsonIgnore.class);

                });

```

### StringUtils

#### 导入

注意是lang3包下面的
