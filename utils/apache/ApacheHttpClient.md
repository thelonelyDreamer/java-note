### 1. 相关操作

#### 1.1 Get请求

```java
public void get() throws IOException {
        // 创建HttpClient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();
        // 创建HttpGet请求
        HttpGet httpGet = new HttpGet("https://www.baidu.com");
        // 响应对象
        CloseableHttpResponse response = null;
        try {
            // 使用HttpClient发起请求
            response = httpClient.execute(httpGet);
            // 判断响应状态码是否为200
            if (response.getCode() == 200) {
                // 获取返回数据
                HttpEntity httpEntity = response.getEntity();
                String content = EntityUtils.toString(httpEntity, "UTF-8");
                // 打印数据长度
                log.info("content:{}", content.length());
            }
        } catch (ParseException e) {
            throw new RuntimeException(e);
        } finally {
            // 释放连接
            if (response != null) {
                response.close();
            }
            httpClient.close();
        }
    }
```

#### 1.2 带参数的Get请求

```java
// 采用字符串拼接
StringBuilder builder = new StringBuilder("https://www.baidu.com");
String url = builder.append("?name=").append("张三").toString();
String encode = URLEncoder.encode(url);
System.out.println(encode);
HttpGet httpGet = new HttpGet(url);
```

#### 1.3 post 请求

```java
// 创建HttpClient对象
CloseableHttpClient httpClient = HttpClients.createDefault();
// 创建HttpPost对象，设置url访问地址
HttpPost httpPost = new HttpPost("https://fanyi.baidu.com/langdetect");

// 声明List集合，封装表单中的参数
List<NameValuePair> params = new ArrayList<NameValuePair>();
// 实际请求地址：https://fanyi.baidu.com/langdetect?query=Java
params.add(new BasicNameValuePair("query", "Java"));

// 创建表单的Entity对象,第一个参数是封装好的表单数据，第二个参数是编码
UrlEncodedFormEntity formEntity = new UrlEncodedFormEntity(params, StandardCharsets.UTF_8);
//设置表单的Entity对象到Post请求中
httpPost.setEntity(formEntity);

CloseableHttpResponse response = null;
try {
    // 使用HttpClient发起请求，获取response
    response = httpClient.execute(httpPost);
    // 解析响应
    if (response.getCode() == 200) {
        String content = EntityUtils.toString(response.getEntity(), "utf8");
        log.info("content={}", content);
    }
}catch (ParseException e) {
    throw new RuntimeException(e);
} finally {
    // 关闭资源
    response.close();
    httpClient.close();
}
```

### 2. 连接池

#### 2.1 连接池管理器

```java
PoolingHttpClientConnectionManager poolingHttpClientConnectionManager = new PoolingHttpClientConnectionManager();
// 设置最大连接数
poolingHttpClientConnectionManager.setMaxTotal(100);
// 设置每个主机的最大连接数
poolingHttpClientConnectionManager.setDefaultMaxPerRoute(10);
// 获取客户端
CloseableHttpClient httpClient = HttpClients.custom().setConnectionManager(poolingHttpClientConnectionManager).build();
```



