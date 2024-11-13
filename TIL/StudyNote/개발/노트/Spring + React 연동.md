#### React
---
1. 프록시 모듈 `http-proxy-middleware` 설치
```
npm install http-proxy-middleware --save
```
2. /src/setupProxy.js 파일 생성
```
const { createProxyMiddleware } = require('http-proxy-middleware');

module.exports = function(app) {
app.use(
    '/api',
    createProxyMiddleware({
    target: 'http://localhost:8080',
    changeOrigin: true,
    pathRewrite: {
        '^/api': '', 
    },
    })
);
};
```
3. axios 요청
```
  useEffect(() => {
    axios.get('/api/v1/main')
    .then(response => setHello(response.data))
    .catch(error => console.log(error))
  }, []);
```
4. 서버 설정
```
@RestController  
@RequestMapping("/v1")  
public class TestController {  
    @RequestMapping("/main")  
    public String test() {  
        return "Test Connected";  
    }  
}
```

```
# WebConfig.java
@Configuration  
public class WebConfig implements WebMvcConfigurer {  
    @Override  
    public void addCorsMappings(CorsRegistry registry) {  
        registry.addMapping("/api/**")  // /api로 시작하는 모든 경로  
                .allowedOrigins("http://localhost:3001")  // React 앱 주소  
                .allowedMethods("GET", "POST", "PUT", "DELETE")  // 허용할 HTTP 메소드  
                .allowedHeaders("*");  // 모든 헤더 허용  
    }  
}
```
