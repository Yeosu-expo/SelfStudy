# 8-1 경로를 다루는 Routers
## DRF 실행 흐름
1. 클라이언트(웹 브라우저, 프로그램 등..)에서 서버에 요청을 보냄
2. urls.py에서 요청(view만 작성해도 Routers라는 클래스가 urls.py를 작성함)
3. view를 실행
4. 필요에 따라 model을 참조(html이 필요없기 때문에 template을 사용하지 않음)
5. view에서 클라이언트에 응답함

[DRF 공식문서](https://www.django-rest-framework.org/)

## Router
* view를 정의해주는 것만으로도 urls.py에 url을 정의해준다.