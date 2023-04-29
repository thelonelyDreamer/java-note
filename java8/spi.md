# spi(*Service Provider Interface*) 机制

## 1. 机制介绍

1. 服务发现机制，为某个接口寻找服务实现的机制，将装配的控制圈移到程序之外。
2. 目的是解耦，为系统提供更为灵活的实现



## 2. 具体实现

### 2.1 接口模块

1. 定义接口

```java
public interface Logger {
    String ROOT_LOGGER_NAME = "ROOT";

    String getName();

    boolean isTraceEnabled();

    void trace(String var1);

    boolean isDebugEnabled();

    void debug(String var1);

    boolean isInfoEnabled();

    void info(String var1);
}
```

2. 寻找服务

```java
public final class LoggerFactory {
	Logger logger = null;
    ServiceLoader<Logger> load = ServiceLoader.load(Logger.class);
    Iterator<Logger> iterator = load.iterator();
    if(iterator.hasNext()){
        logger=iterator.next();
    }
    return logger;
}
```

### 2.2 具体实现

- META_INF
  - services
    - 接口命名的文件（内容为实现类的全限定名）

```java
public class LoggerImpl impl Logger{
    ...
}
```

