### 1. 下列代码输出为

```java
 public static  class  Obj{
    public Obj0 o =new Obj0();
    {
        System.out.println("123");
    }
    public Obj() {
        System.out.println("obj");
    }
}

public static class  Obj0{
    public Obj0() {
        System.out.println("obj0");
    }
}

public void main(){
    new Obj()
}
```

```
obj0
123
obj
```

