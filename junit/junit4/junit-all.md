```
@Before
    public void setUp() throws Exception {
        System.out.println("setup");
    }

    @After
    public void tearDown() throws Exception {

    }
    @Test
    public void test() {
       System.out.println("test");
    }

    @Test
    public void testMain(){
        System.out.println("maintest");
    }
}
setup
maintest
teardown
setup
test
teardown
```

要以类名加Test结尾的类才能被maven打包测试

