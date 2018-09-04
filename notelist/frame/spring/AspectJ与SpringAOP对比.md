## AspectJ与SpringAOP对比

### Spring-AOP Pros

- It is simpler to use than AspectJ, since you don't have to use LTW (load-time weaving) or the AspectJ compiler.
- This can be change to AspectJ AOP when you use @Aspect annotation based Spring AOP.
- This use Proxy pattern and Decorator pattern

### Spring-AOP Cons

- This is proxy-based AOP, so basically you can only use method-execution pointcut.
- Aspects aren't applied when calling another method within the same class.
- There can be a little runtime overhead.
- Spring-AOP cannot add an aspect to anything that is not created by the Spring factory

### AspectJ Pros

- This supports all pointcuts. This means you can do anything.
- There is less runtime overhead than that of Spring AOP.

### AspectJ Cons

- Be careful. Check if your aspects are weaved to only what you wanted to be weaved.
- You need extra build process with AspectJ Compiler or have to setup LTW (load-time weaving)