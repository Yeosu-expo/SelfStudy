# 3-1 QuerySet API란?
Model과 같이 장고의 ORM

* Query: DB에 정보를 요청하는 것
* QuertSet: DB에서 전달 받은 객체의 목롤
* QuerySet API: DB에 요청하기 위한 인터페이스
[QuerySet API 공식문서](https://docs.djangoproject.com/en/4.0/ref/models/querysets/)

## QuerySet API 주요 함수
### 새 QuertSet를 반환하는 메서드
* filter()
  * 매겨변수와 일치하는 개체를 반환함.(값이 여러개이면 여러개 반환)
* exclude()
  * 매개변수를 포함하지 않는 개체를 반환함.(값이 여러개이면 여러개 반환)
* order_by()
  * 매개변수의 필드를 내림차순 혹은 오름차순으로 정렬함.(주로QuerySet를 반환하는 함수와 같이 쓰임.)
* select_related()
* prefetch_related()
* raw()

### QuerySets를 반환하지 않는 메서드
* get()
  * 하나의 데이터를 찾는 함수.(2개 이상이면 오류가 뜸)
* create()
  * 매개변수에 값을 넣어 해당 값을 가지는 개체를 생성
* count()
* first()
* last()
[QuerySet API 공식문서2](https://docs.djangoproject.com/en/4.0/ref/models/querysets/#queryset-api-1)

## Django shell
* 파이썬 인터프리터 형식으로 장고 사용
* Model을 import하여 사용 가능
* python manage.py shell

## Database Tool
* 데이터베이스에 관리를 위한 도구
* 툴을 활용하여 테이블이나 데이터를 조작
* GUI제공

# Admin이란?
setting.py에 app으로 admin이 등록이 되어 있고, urls.py에 admin이 path로 등록되어 있으면, 관리자 인터페이스로 모델을 관리하고 다른 어드민의 설정 및 권한(각 모델 혹은 전체의 CRUD)을 변경할 수 있다.

참고: 모델의 데이터에 변경이 되면 makemigrations 후에 migrate해야 변경된 내용을 적용하여 Model을 추가하고 수정할 수 있다.