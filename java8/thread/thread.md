### 1. 线程的创建
1.1 继承Thread重写run方法
```java
public class DemoCreateThread extends Thread {
    @Override
    public void run() {
        try {
            doSomething();
            this.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        DemoCreateThread thread= new DemoCreateThread();
        thread.start();
    }
}
```
1.2 使用Runnable接口
```java
new Thread(new Runnable() {
    @Override
    public void run() {
        doSomething();
    }
}).start();
```
1.3 使用Callable接口
```java
Callable<String> callable = new Callable<String>() {
    @Override
    public String call() throws Exception {
        return "Hello World";
    }
};
FutureTask<String> futureTask = new FutureTask<>(callable);
new Thread(futureTask).start();
try {
    futureTask.get();
} catch (InterruptedException e) {
    throw new RuntimeException(e);
} catch (ExecutionException e) {
    throw new RuntimeException(e);
}
```

### 2. 线程属性
#### 2.1 daemon
当虚拟机内没有非守护线程时，会自动关闭守护线程，当虚拟机有非守护线程时，不会自动关闭
```java
Thread thread = new Thread();
thread.setDaemon(true);//设置为守护线程
```
#### 2.2 priority
线程优先级，范围为1-10，默认为5，越大优先级越高，虚拟机调度线程的策略

#### 2.3 name 
线程名字

#### 2.4 group
线程组

#### 2.5 contextClassLoader
类加载器

#### 2.6 uncaughtExceptionHandler
未捕获异常处理器

#### 2.7 id
线程的标识符。线程ID是创建此线程时生成的一个正数。线程ID是唯一的，并且在其生命周期内保持不变。当一个线程被终止时，这个线程ID可以被重新使用。
```java
thread.getId()
```

#### 2.8 state
```java
public enum State {
    //线程被调用，还没有start方法
    NEW,

    //正在虚拟机中执行，但是在可能在等待操作系统的其他资源，例如CPU
    RUNNABLE, 不可被中断
    //为进入同步块等待一个监视锁或者重新进入同步块
    // Object#wait()被唤醒后
    // synchronized
    BLOCKED, // 可被中断+

    // 等待另外一个线程唤醒，可被中断
    // condition.await()
    // object.wait()
    // thread.join()
    // LockSupport.pack()
    WAITING,

    //有限等待 // 可被中断
    //Thread.sleep
    //object.wait(long)
    //thread.join(long)
    //ockSupport.parkNanos
    //ockSupport.parkUntil
    TIMED_WAITING,
    // 线程执行完毕
    TERMINATED;
}

```
