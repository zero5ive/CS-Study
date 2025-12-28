# CI/CD(Continuous Integration/Delivery & Deployment)
CI/CD는 애플리케이션 개발 단계부터 배포까지의 모든 단계를 자동화를 통해서 좀 더 효율적이고 빠르게 사용자에게 배포할 수 있는 개념이다.

CI/CD는 코드 변경부터 배포까지를 자동화해, 휴먼 에러를 줄이고 빠르고 안정적인 서비스 제공을 가능하게 하기 위해 필요하다.

 

# CI(Continuous Integration)
CI(Continuous Integration)는 "지속적인 통합"이라는 의미를 가지고 있다.

애플리케이션의 버그 수정이나 새로운 코드 변경 사항이 주기적으로 빌드 및 테스트되면서 공유되는 레파지토리에 통합(merge)되는 것을 의미한다.

- 개발자가 코드를 push/pr하면 ci가 자동 빌드, 자동테스트를 해주고 테스트 통과시 머지 가능상태를 보장해준다.
- CI는 코드 변경 시 자동 빌드와 테스트를 통해 변경 사항이 기존 코드와 정상적으로 통합되는지를 검증하고, 머지로 인한 장애를 사전에 방지하는 것을 목적으로한다.
 

### CI의 장점

- 코드의 검증에 소요되는 시간이 줄어든다.
- 개발 편의성이 향상된다.
- 항상 테스트 코드를 통과한 코드만 레포지토리에 올라가기 때문에, 코드 퀄리티를 높게 유지할 수 있다.
 

 

# CD(Delivery & Deployment)
CD는 "Continous Delivery, 지속적인 제공" 이라는 의미와 "Continuous Deplyment, 지속적인 배포"라는 두 가지 의미를 가지고 있다.

CI에서 Build와 Test가 완료된 후, 배포 단계에서 릴리스 준비가 되었는지, 그리고 문제가 없는지 검토하는 과정을 거친다.

이 과정을 통해 나온 결론이 "이제 사용자들에게 서비스를 제공해도 되겠다!"라는 결론이 나오게 되면, 수동적으로 배포를 진행하게 되는데 이것이 "Continuous Delivery, 지속적인 제공"이다.

반면에, 준비가 완료되자마자 자동화를 통하여 곧바로 배포를 진행하는 경우를 "Continuous Deployment, 지속적인 배포"라고 부른다.

<img width="1598" height="632" alt="image" src="https://github.com/user-attachments/assets/930160f2-e6e5-4381-a8fe-5ab3f95c505f" />


 


- Continuous Delivery는 ‘언제든 배포할 수 있는 상태’를 보장하는 것이고, Continuous Deployment는 ‘배포까지 자동화하는 것’이다.
- Continuous Delivery는 배포 가능한 상태까지 자동화 한 것이고 Continuous Deployment는 배포자체까지 자동화 한 것이다.
 

### CD의 장점

- 개발자는 배포보다는 개발에 더욱 집중할 수 있도록 도와준다.
- 개발자가 원클릭으로 수작업 없이 빌드, 테스트, 배포까지의 자동화를 할 수 있다.
 

 

# 파이프라인
코드 구축부터 시작해서 배포까지의 일련의 과정들을 CI/CD 파이프라인이라고 한다.

총 3가지의 단계로 구성된다.

 <img width="1434" height="494" alt="image" src="https://github.com/user-attachments/assets/2e0c5ace-192f-4d10-9c4d-722082e22b8f" />



 

파이프라인이 주는 장점은 코드배포까지 좀 더 체계적으로 만드는 점과 테스트가 강제된다는 점이다. 파이프라인 자체내에 테스트가 있기 때문에 테스트가 없으면 코드 머지자체가 안되게 만들 수도 있다.

 

 

 

 

# 빌드
빌드란 사람이 작성한 코드를 컴퓨터가 실행할 수 있는 형태로 만드는 과정이다.

대표적인 예로 webpack이 있다.

웹팩(Webpack)은 웹 애플리케이션을 구성하는 여러 자바스크립트 파일, CSS, 이미지 등을 분석하여 하나 또는 여러 개의 파일(번들)로 묶어주는(번들링하는) 모듈 번들러이다.

<img width="1302" height="650" alt="image" src="https://github.com/user-attachments/assets/17c02825-2554-42d4-8953-6f952917b2c5" />

 

 

 

 

# 테스트
테스트 함수 등 작은 단위를 테스팅하는 단위테스트, 모듈을 통합할 때 테스트하는 통합테스트, 사용자가 서비스를 사용하는 상황을 가정해서 테스트하는 엔드투엔드테스트가 대표적이다.

<img width="1446" height="672" alt="image" src="https://github.com/user-attachments/assets/f5a64473-28a3-4085-b126-64670717b2d1" />

 


 

 

 

# 머지
git이나 svn을 이용해 머지한다. 충돌을 최소화시키는 것이 가장 중요하다.

충돌은 대부분 일어나기 때문에 조금 더 작은 단위로 충돌이 일어나게 하는게 중요하다. 작은 issue단위를 기반으로 머지한다.

 

 

 

# 배포
배포는 그저 사용자를 위한 서비스를 배포할 수도 있다고 생각할 수 있지만 그 뿐만이 아닌 내부적으로 QA엔지니어나 관리자페이지를 위한 배포, 데이터웨어하우스로부터 데이터를 가공해서 백앤드개발자를 위한 배포 등을 포함한다.

 

 

# 툴(배포를 위한 도구)
github action, genkins, circle ci가 유명하며 heroku를 통해 CI, CD 없이 자동 가능 참고로 heroku + github action으로 설정도 가능
