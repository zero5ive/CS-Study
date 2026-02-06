# REST API의 특징
1. Uniform-Interface
API에서 자원들은 각각의 독립적인 인터페이스를 가지며 각각의 자원들이 url 자원식별, 표현을 통한 자원조작, Self-descriptive messages, HATEOAS 구조를 가지는 것을 말함
독립적인 인터페이스라는 것은 서로 종속적이지 않은 인터페이스를 말함

### URL 자원식별
Identification Of Resources를 말하며, 자원은 URI로 식별되어야 함.

### 표현을 통한 자원조작
manipulation of resources through represetations은 url과 GET, DELETE 등 HTTP 표준메서드 등을 통해 자원을 조회, 삭제 등 작업을 섦영할수 있는 정보가 담겨야 하는 것을 말함

### Self-descriptive messages
HTTP Header에 타입을 명시하고 각 메시지(자원)들은 MIME types에 마춰 표현되어야 함. 예를 들어 .json를 반환한다면 application/json으로 명시해주어야 함

### HATEOAS 구조
HATEOAS(Hypermedia as the Engine of Application State)는 하이퍼링크에 따라 다른 페이지를 보여줘야 하며 데이터마다 어떤 URL에서 원했는지 명시해주어야 하는 것을 말함. 보통 href, links, link, url 속성 중 하나에 해당 데이터의 URL을 담아서 표기해야 함

2. Stateless
HTTP 자체가 Stateless이기 때문에 HTTP를 이용하는 것만으로도 만족, 그리고 이는 REST API를 제공해주는 서버는 세션(session)을 해당 서버 쪾에 유지하지 않는다는 의미

3. Cacheable
HTTP는 원래 캐싱이 되며, 아무런 로직을 구현하지 않아도 자동적으로 캐싱이 됨. 새로고침을 하면 304가 뜨면서 원래 있떤 js와 css 이미지 등을 불러오는 것을 볼 수 있음. 이는 HTTP 메서드 중 GET에 한정되며 'Cache-Control:max-age=100'(100초) 이런 식으로 한정된 시간을 정할 수가 있으며 캐싱된 데이터가 유효한지를 판단하기 위해 'Last-modified'와 'Etag'라는 헤더값을 쓰며, 'Etage'는 전달되는 값에 태그를 붙여서 캐싱되는 자원인지를 확인

4. Client-Servcer 구조
클라이언트와 서버가 서로 독립적인 구조를 가져야 함. 물론 이는 HTTP를 통해 가능한 구조이며, 서버에서 HTTP 표준만 지키민다면 웹에서는 그에 따른 화면이 잘 나타나게 됨. 서버는 그저 API를 제공하고 그 API에 맞는 비즈니스 로직을 처리하면 됨. 마찬가지로 클라이언트에서는 HTTP로 받는 로직만 잘 처리하면 되는 것

5. Layered SYstem
계층 구조로 나눠져 있는 아키텍처를 뜻하고, WEB 기반 서비스를 하면 보통 이러한 시스템을 구축하게 됨.

# REST API의 URL규칙
1. 동작은 HTTP 메소드로만 해야 하고 url에 해당 내용이 들어가면 안됨.
수정 = put, 삭제 = delete, 추가 = post, 조회 = get을 이용해야 함 예를 들어 '/books/delete/1' 이렇게 표기하면 안됨
2. .jpg, .png 등 확장자는 표시하지 말아야 함
3. 동사가 아닌 명사로만 표기해야 하며, 윶가 책을 소유한다라는 것을 표현한다면 '유저/유저아이디/inclusion/책/책아이디'로 표현하고 유저가 소유한 아파트를 조회한다고 하면 이렇게 표현해야 하며 /users/{userid}/aparts 또한 /getAllUsers 식의 동사를 집어넣으면 안됨
4. 계층적인 내용을 담고 있어야 함. '/집/아파트/전세' 이런 식으로 내려가야 함
5. 대문자가 아닌 소문자로만 쓰며 너무 길 경우에 바를 써야 할 경우 언더바_가 아닌 그냥 바 -를 씀
6. HTTP 응답 상태코드를 적재적소에 활용해야 함. 성공시에는 200, 리다이렉튼는 301 등..

# Q. 브라우저 렌더링이란?
브라우저는 다음과 같이 브라우저엔진, 렌더링엔진, 네트어크통신부, 자바스크립트 해석기, UI백엔드, 자료저장소로 이루어져 있음
![](https://velog.velcdn.com/images/shypanda0119/post/c49cf3c2-f0f6-442c-a68b-21f85d812ae1/image.png)

#### DOM트리와 CSSOM 트리 구축

- DOM트리 구축
하나의 html 페이지는 div, span 등의 요소를 가지며, 이러한 요소들이 HTML파서에의해 "구문분석" 됨. 그리고 요소는 하나하나가 노드(Node)로 설정이 되어 트리 형태로 저장되는데, 이를 DOM 트리라고 함
![](https://velog.velcdn.com/images/shypanda0119/post/dd517eaf-8999-4560-b404-7972b1afc157/image.png)

- CSSOM 트리 구축
각각의 노드는 CSS 파서에 의해 정해진 스타일 규칙이 적용되어 있음. span.color = "red"는 노드 색깔이 빨간색이다 등을 말함. 이런 것들을 기반으로 CSSOM이라는 트리가 만들어지며, 이 과정은 DOM트리 구축과 "동시에" 일어남.
![](https://velog.velcdn.com/images/shypanda0119/post/51856dfe-4548-45e0-92ce-d24000fee274/image.png)

#### 렌더트리와 렌더레이어 생서
DOM 트리와 CSSOM 트리가 합쳐져 렌더객체(Render Object)가 생성됨. 그리고 이들이 모여 병렬적인 렌더트리가 생성됨
![](https://velog.velcdn.com/images/shypanda0119/post/cb832d0d-de3e-4078-a7d8-1e430e2e8f1a/image.png)
이때, display:none이 포함된 노드는 지워지고 font-size 등 상속적인 스타일은 부모노드에만 위치하도록 설계하는 등의 최적화를 거쳐 렌더레이어가 완성됨.
**중요! display:none은 렌더트리에서 삭제되지만 visibility: hidden은 요소를 보이지 않게 하지만 요소는 여전히 레이아웃에서 공간을 차지.**

![](https://velog.velcdn.com/images/shypanda0119/post/35aa30b6-bd64-41f9-a837-5f2840e3c8b7/image.png)
이 때, 렌더레이어가 완성될 때, GPU에서 처리되는 부분이 잇으면 이 요소들은 각각 강제적으로 그래픽레이어(Graphic Layer)로 분리됨.

#### 렌더레이어를 대상으로 Layout 설정
좌표는 보통 부모를 기준으로 설정되며 Global Layout은 부라우저 사이즈가 증거하거나 폰트 사이즈가 커지면 변경 됨
![](https://velog.velcdn.com/images/shypanda0119/post/c0414be3-6410-429c-86c6-401522213490/image.png)

#### 렌더레이어를 대상으로 칠하기(paint)
픽셀마다 점을 찍듯 칠하며, 이를 레스터화라고도 함.

#### 레이어 합치기(composite layer) 및 표기.
각각의 레이어로부터 비트맵이 생성되고 GPU에 텍스처로 업로드 됨. 그다음은 텍스처들은 서로 합쳐져 하나의 이미지로 렌더링되며 화면으로 출력됨.

