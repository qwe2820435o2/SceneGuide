# ThreadLocal value is disordered

## 1. What happen?

```markdown
One day, someone finds that although the Token has expired, they can still obtain the information after logging in, but the information is not their own

It's so weird, isn't it?

```

## 2. Check
> Recently introduced a new component: gateway, will it be the variable that it brings?