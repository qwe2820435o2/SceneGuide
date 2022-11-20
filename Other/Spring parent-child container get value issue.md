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

# 3. Solution

```markdown
1. Corresponding to the container scan, write a property configuration file
2. Or the parent container injects the attribute, provides getter and setter methods externally, and the child container obtains it through the getter method
```

# 4. Analyze

```markdown
The spring container has the concept of parent-child containers

spingmvc is a child container that stores Controller objects

the spring container is a parent container that stores Mapper proxy objects and Service objects
```