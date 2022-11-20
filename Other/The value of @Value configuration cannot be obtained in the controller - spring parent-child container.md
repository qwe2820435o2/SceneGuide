# 1. Why can not get value
```markdown
In the controller, the value cannot be obtained with the @Value annotation, 
but the ${key} string is directly output
```

# 2. Reason
```markdown
In the project, 
only <context:property-placeholder location="classpath*:properties/*.properties"/> 
is configured in applicationContext.xml, not in spring-mvc.xml
```