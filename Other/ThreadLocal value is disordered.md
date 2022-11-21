# ThreadLocal value is disordered

## 1. What happen?

```markdown
One day, someone finds that although the Token has expired, they can still obtain the information after logging in, but the information is not their own

It's so weird, isn't it?

```

## 2. Check
> Recently introduced a new component: gateway, will it be the variable that it brings?

### 2.1 Overall process

![Overall process](../Material/image/ThreadLocal%20value%20is%20disordered.png)

### 2.2 Reason

```
Our service is deployed in Tomcat and uses thread pool technology

ThreadLocal is used in the service interceptor, which is not a problem in itself, but the information stored in the current thread is not destroyed after each use. 

The next time the request comes, the thread is reused and the data obtained in the last request is obtained.

Example:
The first:  User A -> Gateway -> Service -> interceptor Set A Info -> Get A Info 
The second: User B -> Gateway -> Service -> interceptor No B Info(token expire or other else) -> But still get A Info      

```

### 2.3 Solution

After the request is completed, in the interceptor life cycle method **afterCompletion**, clear the value in ThreadLocal

```markdown
@Override
public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    //ThreadLocal使用完清除，防止被线程复用
    userInfoThreadLocal.remove();
    locationThreadLocal.remove();

    super.afterCompletion(request, response, handler, ex);
}
```