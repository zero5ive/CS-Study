# 오리진과 SOP
#### 오리진
![](https://velog.velcdn.com/images/shypanda0119/post/1b9aa336-57a0-495b-8650-6cde44ebcff7/image.png)

#### SOP(Same-Origin Policy)란?
브라우저 상에서 오로지 같은 오리진끼리만 요청을 허가하는 보안정책
![](https://velog.velcdn.com/images/shypanda0119/post/3d8a0c65-43e8-4eb2-a327-84b16ed76e09/image.png)

SOP가 없다면 어떻게 될까? 예를 들어 은행 계좌서버에 로그인하고 악의적인 사이트를 방문하면 내가 모르는 사이에 은행 서버에 요청을 할 수 있게 되어 내 계정 정보가 변경되거나 유출될 수 있음. 즉, 악성스크립트가 다른 오리진의 서버에 요청을 보내고 사용자의 리소스를 임의적으로 접근할수 있는 것 이를 1차적으로 막아주는 것이 바로 SOP 보안정책

# CORS
#### CORS(Cross Origin Resource Sharing)란?
HTTP 헤더를 기반으로 브라우저가 다른 오리진에 대한 리소스 로드를 허용할지 말지에 대한 메커니즘을 말함
- 리소스: 이미지, CSS, JS, 비디오 등
![](https://velog.velcdn.com/images/shypanda0119/post/9debcfce-3f26-4cd0-98df-0cad2e27159f/image.png)

#### preflight request와 simple request
요청을 보낼 때 다음의 메서드 타입, 헤더에 해당되지 않은게 하나라도 포함이 되어있따면 preflight request를 보내게 됨. 반대로 다음의 메서드 타입, 헤더를 모두 가진 요청을 간단한 요청(simple request)이자 안전한 요청이라고 함.

preflight request과정은 다음과 같이 이루어짐
1. OPTIONS 메서드로 해당 서버에 원래 요청을 보내기 전 요청을 보냄
2. 요청을 받은 서버는 Access-Control-* 헤더로 응답
3. Access-Control-* 헤더에 요처한 오리진이 존재하지 않는다면 CORS 에러를 보내게 됨

#### Access-Control-Allow-Origin
cors라는 미들웨어를 사용하지 않는다면 직접 다음과 같이 header에 추가해서 설정할 수 있음
```
app.use((req, res, next) => { 
res.header("Access-Control-Allow-Origin", "*");  
res.header("Access-Control-Allow-Origin", 
"https://example.com");   
}); 
```

#### CORS 미들웨어의 내부 코드
CORS 미들웨어는 Access-Control-Allow-Origin을 쉽게 설정해주는 미들웨어라고 보면 됨
```
function configureOrigin(options, req) { 
	var requestOrigin = req.headers.origin, 
	headers = [], 
    isAllowed; 
 
    if (!options.origin || options.origin === '*') { 
      // allow any origin 
      headers.push([{ 
        key: 'Access-Control-Allow-Origin', 
        value: '*' 
      }]);
```

