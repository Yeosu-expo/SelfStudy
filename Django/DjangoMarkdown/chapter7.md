# 7-1 API와 DRF란?
## API
* Application Programming Interface 응용 프로그램 프로그래밍 인터페이스
* **컴퓨터 프로그램(또는 컴퓨터) 사이**의 **상호 작용**을 하기 위한 **인터페이스** 사양을 의미
>> API는 사용자(클라이언트)가 아닌 프로그램을 위한 기능

### API 종류
* Public API(공개)
  * 누구나 사용할 수 있는 오픈 API
* Private API(비공개)
  * 서비스 개발 등 내부적으로 사용하는 API

#### Public API를 사용하는 이유
* 직접 개발을 할 수 없거나 필요한 데이터를 사용 등(지도, 윈도우, 날씨같은 공공데이터 등)
  * 프로그램 개발마다, 윈도우 같은 운영체제를 개발하고 할 수 없고, 지도가 필요해서 지도를 개발할 수 없다. 그래서 Public API가 사용된다.

#### Private API를 사용하는 이유
* 모바일 앱, AJAX, SPA 등 기능 수행이나 데이터가 필요한 경우 등
  * AJAX(좋아요 기능같은 특정 데이터만을 받기 위해 새로고침이나, 페이지 이동 등을 제한하는 기술)

### API 사용 과정
![api](./img/api%20rin.png)
1. 프로그램에서 API서버에 API를 요청함
2. API서버가 필요한 기능이나 데이터를 요청해서 받아옴
3. 받아온 기능이나 데이터를 프로그램에 전달함
>> 프로그램 입장에서는 API 서버에 어떤 기능이 있는지 모름

## DRF
* Django REST framework
* DRF는 장고를 기반으로 웹 API 구축할 수 있도록 기능 등을 만들어 놓은 툴킷

# 7-2 RESTful한 API는 무엇인가요?
## API는 어떤 기준으로 개발해야 하는가?
**개발자 간의 협력**과 **유지보수 및 확장에 용이**한 개발을 위해 개발해야 함

## REST API
* REpresentational State Transfer
* HTTP 통신에서 어떤 자원에 대한 CRUD 요청을 Resource(자원)와 Method(행위)로 표현하여 특정한 형태로 전달하는 방식
* REST 설계 규칙을 잘 지켜서 설계된 API를 ‘RESTful 하다’ 표현

### REST API 특징
* 균일한 인터페이스
  * 아키텍처를 단순화하고 상호 작용의 가시성을 향상 시킴
* 무상태 
  * 클라이언트에서 서버로의 각 요청에 요청을 이해하고 완료하는데 필요한 모든 정보가 포함되어야 함
* 캐시 처리 가능 
  * 클라이언트는 응답을 캐싱할 수 있어야함
* 계층화
  * 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 등을 위한 계층을 추가하여 구조를 변경할 수 있음.
  * Proxy, Gateway와 같은 네트워크 기반의 중간매체를 사용할 수 있게 해주며 클라이언트는 서버와 직접 통신하는지, 중간 서버와 통신하는지 알 수 없음
  * 즉, API에서 다른 API로 필요한 정보를 또 요청한다는 것이다.(하청의 하청이라고 생각하면 편함)
* 클라이언트/서버 구조 
  * 아키텍처를 단순화시키고 작은 단위로 분리함으로써 클라이언트-서버의 각 파트가 독립적으로 구분하고 서로 간의 의존성을 줄임

### REST API 설계 규칙
1. URI는 명사를 사용
2. 슬래시(/)로 계측 관계를 표현
3. 밑줄(_)을 사용하지 않고, 하이픈(-)을 사용
4. URI는 소문자로만 구성
5. HTTP 응답 상태 코드 사용
6. 파일확장자는 URI에 포함하지 않음
[RESTful 설계 규칙 공식문서](https://restfulapi.net/rest-api-design-tutorial-with-example/)

### HTTP Method 역할
* POST 
  * POST를 통해 해당 URI를 요청하면 리소스를 생성
* GET 
  * GET을 통해 해당 리소스를 조회
* PUT 
  * PUT을 통해 해당 리소스를 수정
* PATCH 
  * PATCH를 통해 해당 리소스를 부분 수정
* DELETE 
  * DELETE를 통해 해당 리소스를 삭제

#### URI, URL
* URI
  * URI(Uniform Resource Identifier)는 특정 리소스를 식별하는 통합 자원 식별자를 의미 인터넷에 있는 자원을 나타내는 유일한 주소
* URL
  * URL(Uniform Resource Locator)은 흔히 웹 주소라고도 하며 컴퓨터 네트워크 상에서 리소스가 어디 있는지 알려주기 위한 규약
>> URL의 주소에서 특정 id나 파일의 주소를 붙여지는 주소를 URI라고 보면 된다.(URL은 URI임, 반대는 그럴 수도 아닐 수도)

# 7-3 Django REST Framework(DRF)란?
* DRF개발은 API서버와 그 안에 기능을 구현한다는 것
* 또, 클라이언트(프로그램)가 모바일, 웹 등에 구애받지 않고, 기능을 수행 함
* 클라이언트 단에서는 API의 응답 정보에 대한 처리만 구현하면 됨
* 장고에 기본 기능이 아니라, 서브파티이기 때문에, 장고 공식문서에는 DRF에 대한 내용이 없음

[DRF공식문서](https://www.django-rest-framework.org/)

## DRF
* Django REST framework
* DRF는 장고를 기반으로 웹 API 구축할 수 있도록 기능 등을 만들어 놓은 툴킷
* RESTful한 API형태의 기능을 제공
* CBV를 사용해야 쉽게 구현 가능

>> 역할: 클라이언트에게 받은 요청을 처리, 응답

### DRF 장점
* API, 개발을 쉽게 만들어 줌
* 인증 정책 OAuth1, OAuth2 사용 가능
* **Serializer(직렬화) 기능을 제공**(Model > JSON, JSON > Model)
* 문서화, 커뮤니티 지원

### DRF 핵심 요소
* 요청/응답
* View와 ViewSet
* 라우터
* 직렬화
* 인증/권한
* 페이징/필터

### 서브파티:Postman
* 백엔드 개발자들이 테스트를 위해 그때마다 프론트엔드를 제작하는 것은 번거롭다
* 그렇기 때문에 GET, POST 등의 요청을 보내주는 프론트엔드의 기능을 가진 앱이 필요 >> Postman
* 만약 클라이언트 단에서 요청을 날렸는데, 오류가 났을 때, Postman으로 요청을 해서 오류가 없다면, 클라이언트 단에서 오류가 났음을 시사하고, 반대의 경우에는 백엔드 문제를 시사함.(활용 방법)

##### tips
* CBV로 view.py를 구현하면, GET요청은 get이라는 이름의 함수로 매개변수는 self, request로 함.
* POST요청도 post라는 함수를 정의해서 처리 