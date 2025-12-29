# CI/CD(Continuous Integration / Delivery & Deployment)란?
 지속적으로 코드를 합치고 코드를 배포하는 것
 
####  파이프라인이란?
 코드 구축부터 시작해서 배포까지의 일련의 과정들을 CI/CD 파이프라인이라고 함
![](https://velog.velcdn.com/images/shypanda0119/post/0e455874-0219-4e7c-b5cf-6898f563e12f/image.png)
continuous intergration : 코드를 빌드하고 테스트하고 합침
continuous delivery : 해당 레퍼지토리에 릴리스함
continuous deployment: 이를 프로덕션, 즉 실제 서비스에 배포
 
####  빌드
![](https://velog.velcdn.com/images/shypanda0119/post/abd8c2e1-a30a-4d15-aa25-770332aeb8c4/image.png)
대표적으로 wepback이 있음

#### 테스트
함수 등 작은 단위를 테스팅하는 단위테스트, 모듈을 통합할 때 테스트하는 통합테스트, 사용자가 서비스를 사용하는 상황을 가정해서 테스트하는 엔드투엔드 테스트
대표적으로는  mocha 프레임워크가 있음

#### 머지
git이나 svn을 이용해 머지를 함.

#### 배포
사용자를 위한 서비스를 배포할 수도 있다고 생각할 수 있지만 그뿐만이 아닌 내부적으로 QA엔지니어나 관리자페이지를 위한 배포, 데이터웨어하우스로부터 데이터를 가공해서 백엔드개발자를 위한 배포 등을 포함

#### 툴
github action, genkins, circle ci가 유명하며 heroku를 통해 CI, CD 설정 없이 자동 가능
