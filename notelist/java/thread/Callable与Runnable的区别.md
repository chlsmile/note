## Callable与Runnable对比

### 相似之处
- Callable与Runnable接口大致相似，都是用于多线程，Callable接口有一个方法是call()方法，Runnable接口中有一个方法是run()方法

### 不同之处
- Callable中的call()方法有返回值， 而Runnable接口中的run()方法没有返回值
- Callable中的call()方法会抛出一个checked Exception，而Runnable接口中的run()方法不会抛出checked Exception

