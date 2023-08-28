본 문서는 노션에서 마크다운으로 내려온 것으로, 가독성이 떨어질 수 있습니다.
[본문](https://www.notion.so/HTML-05ff7ff17f934db9b2f21f9104144389?pvs=4
)
# HTML

<!DOCTYPE html>: HTML5 문서임을 명시함

<head>: 보여지는 부분이 아닌 직접적으로 표현되지 않는 정보(메타데이터)를 정의함. <html>태그 <body>태그 사이에 위치함 ex) title, style, meta, link> script, base

title: 웹페이지의 이름을 정의

body: 웹페이지에 직접적으로 보여지는 부분. <head>태그 아래에 위치해야함

meta: 문서에 대한 설명임. <head>태그안에 들어가고 주로 charset=”utf-8”을 표시해 한글이 깨지지않게 함.

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled.png)

속성명은 소문자로 쓴다. 대소문자가 구분되지 않는다.

속성값은 따옴표로 감싼다. 속성값이 여러개일때는 ;(세미콜론)으로 구분

## html의 텍스트 태그들

### <h#>~</h#>

h1~h6까지 있고 숫자가 작아질 수록 더 큰 텍스트를 갖고, 중요도를 나타낸다.

### p

paragraph의 약자로, 하나의 문단을 만들 때 쓰임 이전 요소에 하나의 공백의 간격을 가짐.

### br

줄바꿈 태그이다. html은 태그안에서 엔터를 눌러도 줄바꿈으로 인식하지 않기 때문에 사용됨

### hr

Horizontal Rules의 약자로 내용과 내용사이에 선으로 분리되게 해준다. ex) 내용 hr 내용 

### pre

preformatted Text의 약자로 html은 탭이나 스페이스바를 여러번 입력해도 하나의 공백만 인식한다. 또, 줄바꿈을 인식하지 못한다. 하지만 pre태그로 감싼 내용은 입력한 형태 그대로 적용된다. 즉, 줄바꿈 여러공백을 전부 인식한다.

### b와strong

b는 bold의 약자로 텍스트를 굵은 텍스트로 나타냄 strong태그도 마찬가지이지만 의미적으로 중요할 때 사용됨

### i와em

둘다 이텔릭체로 변환시켜준다. 이텔릭체는 기울여쓰는 것임. 위의 태그와 마찬가지로 em이 의미적으로 더 중요할 때 사용됨. 추가적으로 html5에서부터 i태그가 css와 함께쓰이면 이텔릭체 뿐만 아니라 다른 글꼴로 바꿀 수 있음

### small

텍스트를 작게 출력하는 태그

### sup와 sub

sup태그는 super subscript의 약자로 윗첨자를 나타내고, sub은 subscript의 약자로 아래첨자를 나타냄. 윗첨자는 제곱처럼 텍스트를 표시한다고 생각하면되고 아래첨자는 반대이다.

### mark

텍스트에 노란 형관펜으로 강조함

### ins와 del

ins insert의 약자로 텍스트에 밑줄을 그음. del delete의 약자로 텍스트에 취소선을 그음

### q와 blockquote

q quote의 약자로 짧은 인용문을 쓸때 사용한다. 텍스트를 큰 따옴표로 감쌈. blockquote는 긴 인용글을 쓸때 사용하는데 전체 글이 전부 탭으로 들여써져서 표현됨.

### 주석(Comment Tag)

<!— 주석내용 —>으로 사용함

### abbr

abbreviation의 약자로 축약어에 마우스를 올리면 뜻풀이가 나온다. 사용법은 title속성명에 뜻풀이를 적고 시작태그와 종료태그사이에 축약어를 쓰면된다.

## HTML Links

### 사용법

<\a href=”링크주소”>텍스트</\a>이다

- <\a>: anchor의 약자이고, 하이퍼링크를 의미
- 텍스트: 인터페이스에 링크주소가 표시되는 것이 아닌 텍스트내용이 표시되고, 텍스트를 누르면 링크로 이동이 된다.
- href: <\a> 태그의 주요 속성으로 Hypertext Reference의 약자로 텍스트를 클릭했을 때 이동할 주소를 속성값으로 가짐.

### target 속성

기본적으로 하이퍼링크 텍스트를 클릭하면 현재 창에서 주소창으로 이동한다. 이를 변경해주기 위해 target속성이 필요하다. 다음은 target의 속성값이다.

- _self: 디폴트 값으로서, 해당창에서 주소창으로 이동함.
- _blank: 현재창이 아닌, 새로운 창에서 주소창으로 이동.
- [ ]  _parent: 만약 창을 여러개 열어놨다면 바로 이전에 열어둔 창에서 주소를 연다.
- [ ]  _top: 여러개의 창중에 가장 최근에 열어본 창에서 이동

### Link State

링크의 상태를 4가지로 나타낼 수 있다.

- link: 한번도 열어본적이 없는 상태. 디폴트 값이며 파란색으로 표시됨
- visited: 방문한적이 있는 상태로 보라색으로 표시됨
- hover: 링크위에 마우스가 올려진 상태로 빨간색으로 표시됨
- active: 링크를 마우스로 누른 상태로 CSS로 색을 지정할 수 있음

위의 상태에서 색은 모두 css를 통해 조정할 수 있음. 밑줄을 없앨 수도 있음. 

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%201.png)

위의 예시처럼 css에서 조정할 수 있음.

### Bookmarker

책갈피 개념으로 <a>태그로 표시한 링크를 클릭하면 해당 웹에서 지정한 곳으로 이동한다. 새로운 페이지로 이동하는 개념이 아닌 현재 페이지에서 시선을 이동시켜주는 개념이다. 사용하는 방법으로는 href속성의 속성값으로 id나 name 속성을 명시해주면 된다.

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%202.png)

## HTML Image

<img>태그를 사용하여 활용할 수 있으며. end tag가 없는 empty tag임

### 사용법

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%203.png)

속성값

- src : source의 약자로 표시할 이미지의 URL주소를 입력함.
- alt : alternative의 약자로 표시할 이미지가 주소의 오류나 서버의 다운등 여러 이유로 이미지를 불러오기 어려울 때, 대체할 이미지를 보여준다.
- width : 숫자를 입력해 이미지의 가로길이를 조절한다.
- height : 숫자를 입력해 이미지의 세로길이를 조절한다.

a태그로 img태그를 감싸고 a태그 안에 주소를 입력하면 이미지를 클릭하면 a태그 안에 링크로 이동한다. ex) <\a href=”주소”><\img src=”주소”></\a>

### 경로(src)

- 절대경로

객관적으로 언제나 동일한 경로, 즉 표시하고자 하는 위치가 가지는 고유한 경로이다. 예를 들어 컴퓨터에 저장된 파일을 표시할 때는 C:\을 포함해 그 파일의 위치까지를 나태내고 주소는 [http://로](http://로) 시작한다. 

- 상대경로

절대경로와 다르게 현재 위치해 있는 곳을 기준으로 표시하고자하는 파일의 주소를 나타낸다. 예를 들어 web이라는 폴더 안에 html과 img폴더가 있고 html폴더 안에 link.html이 있고 img폴더 안에 img1.png파일을 가르키고자 할때 ../img/img1.css라고 가르킨다.

- /: 최상위 디렉토리로 이동한다.
- ./: 현재 위치한 디렉토리를 의미한다.
- ../: 상위 디렉토리로 이동한다.

## HTML List

텍스트나 데이터 등을 순차적으로 나열하는 기능이다. 이것을 List라고 하고 3가지의 종류가있다.

- 순서가 없는 리스트(unordered list)
- 순서가 있는 리스트(ordered list)
- 정의 리스트(definition list)

### 순서가 없는 리스트(unordered list)

ul : unordered list의 약자이고, 검은색 점으로 항목을 구분한다.

li : ul태그 안에 각 항목을 표시하는 태그이다.

CSS를 활용하여 다음과 같이 4가지 디자인으로 검은색 점을 바꿀 수 있다.

- disc : 디폴트 값으로 검은색 점이다.
- circle: 원
- square: 사각형
- none: 아무것도 표시되지 않는다.

또한 리스트 안에 리스트를 넣어 중첩 시키는 방법이 가능하다. 각 리스트는 들여쓰기로 구분된다.

### 순서가 있는 리스트(ordered list)

ol : ordered list의 약자이고, 숫자로 순서를 표시한다. 

li : ol태그 안에서 각 항목을 구분한다.

type속성 : 이 속성을 활용하여 순서를 숫자가 아닌 것으로도 표현할 수도 있다.

- 1 : 디폴트 값으로 아라비아 숫자이다.
- A: 대문자 알파벳
- a: 소문자 알파벳
- I: 대문자 로마숫자.
- i: 소문자 로마숫자.

start속성 : 이 속성을 활용하면 시작 숫자를 바꿀 수 있다.

ordered list또한 중첩할 수 있다.

### 정의 리스트(definition list)

주로 용어와 용어설명을 위해 사용된다.

dl : definition list의 약자이고, 리스트의 시작태그다.

dt : 설명할 용어를 입력

dd : 용어에 대한 설명을 입력

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%204.png)

### HTML Table

table : table의 시작을 알리는 태그 사실상 워드프로그램 표랑 비슷하다.

thead : 표에서 최상단 행. 테이블에서 전체 헤더 항목을 감쌈

th : thead에서 헤더 항목을 표시

tbody : tr태그를 감쌈

tr : 하나의 행 즉, 가로방향으로 정보를 입력

td : tr태그에서 해당 행에서 왼쪽에서 오른쪽 순으로 텍스트 입력

이해를 위해 이미지 첨삭

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%205.png)

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%206.png)

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%207.png)

<합치고 싶은 행 colspan=”해당 행에서 열을 합치려고 하는 칸의 수” > 텍스트 tag으로 해당 행 안에서 지정한 숫자의 수 만큼 열을 합칠 수 있음 반대의 경우에는 속성으로 rowspan을 쓰면 됨.

caption : table태그 사이에 넣어서 caption태그 안에 텍스트를 입력하면 테이블 위에 제목처럼 표시할 수 있다.

---

HTML에는 크게 두가지 요소가 있음 

1. 블록(block)
2. 인라인(inline)

블록(block)은 언제나 새로운 라인에서 시작하며 해당라인을 전부 차지함. 

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%208.png)

여기서 div는 여러 요소들을 한데 묶어 한번에 관리하기 위해서 사용된다.

인라인(inline)은 새로운 라인에서 시작하지 않고, 해당 내용만큼의 공간만 차지한다. 

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%209.png)

span은 하나의 텍스트에서 따로 구분지어 편집하기 위해 사용된다.

iframe(inline frame), frame은 둘다 웹 페이지 주소를 불러오게 할 수 있는 태그이다. 둘의 차이점은 모르겠담. but HTML5에서 frame은 사리지고 iframe은 남았다..

frame태그로 창을 수평 혹은 수직방향으로 분리할 수 있음.

iframe태그로 여러개의 웹 페이지 삽입하는 방법은 a태그로 주소를 불러오고 target속성의 값을 iframe의 name속성값과 같게하면 a태그로 불로온 주소를 누르면 iframe의 창에서 열게 된다.

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%2010.png)

레이아웃을 하는 방법으론 div, html5레이아웃, table이 있는데 주로div와 css를 활용하여 레이아웃하는게 자주 사용되고 table은 구식이라 사용하지 않는 것이 좋다…

html에서는 사용자에게 입력을 받을때는 form과 input을 활용하여 입력 받는다.  

### form

end tag가 있고 입력받은 데이터를 서버로 보내주는 역할을 한다. 

- action 속성 : 입력 받은 데이터를 처리할 URL을 입력
- method 속성 : 입력 받은 데이터를 서버에 전달할 방식을 명시함.

GET방식 : 클라이언트에서 서버에 데이터를 불러오고자 할때 사용된다. 

POST방식 : 변경된 데이터나 입력받은 데이터를 서버에 전송하고자 할때 사용됨. 보안성 및 활용성이 GET방식보다 높다.

### input

주로form태그 안에서 실행하며, input은 사용자로 부터 데이터를 입력받을 수 있는 태그이다.

type 속성 : 데이터를 입력받을 방법을 지정해준다.

name 속성 : 이름을 명시해주는 태그로 무조건 써주는게 좋음.

placeholder 속성 : 입력받는 창에 무엇을 입력해야할지 메세지를 입력할 수 있는 속성이다. 클릭 후에는 다시 아무것도 보이지 않는다.

### <input> type속성값들….

text: 문자열 형태로 입력을 받음.

password: 입력받은 텍스트를 클라이언트 화면상에 지정된 문자로만 보이게 한다. **********

- radio: 체크형태의 입력방식이다. 밑에는 radio속성과 같이 쓰이는 속성들임.
    
    checked 속성 : 초기화면에서 체크박스를 체크된 상태로 만든다.
    
    name 속성 : 보통 체크형태의 입력은 여러 선택지가 있기 때문에 같은 선택지 안에서는 서로 같은 선택지라는 것을 명시하기 위해 쓰임. 반드시 같은 선택지 안의 radio속성들은 같은 name속성값을 가져야함.
    
    value 속성 : 클라이언트에 나오지는 않지만 값을 명시함.
    
- checkbox : radio속성과 같이 체크형태의 입력방식이나, 여러개의 선택을 받을 수 있다.
    
    checked 속성 : 초기화면에서 체크되어 표시됨,
    
    name 속성 : 이름을 명시해 주어 같은 체크박스 타입 선택지안에서는 같은 이름을 가져야함.
    
    disabled 속성 : 해당 옵션을 선택할 수 없게 해줌.
    
- file : 파일을 업로드하는 식의 입력방식이다.
    
    accept 속성 : 입력받을 파일의 확장자 및 종류를 명시할 수 있음.
    
- textarea : input태그의 속성이 아니지만 메모장의 형태로 여러줄의 텍스르를 입력할 수 있다.
    
    rows, cols 속성 : 입력칸의 높이와 너비를 조절할 수 있다.
    
- select : input태그 없이 사용되며, 선택지를 리스트 형태로 보여주어 입력 받는다. 태그안에 option태그로 리스트를 구성함.
    
    selected 속성 : 초기화면에서 선택되어 표시됨.
    
    size 속성 : size속성값의 숫자크기만큼 화면에 선택지가 표시됨. size를 명시해주지 않으면, 드롭다운 형태로 표시됨.
    

button 속성 : 클릭으로 입력받음. button태그와 유사함.

submit 속성 : button속성과 기능적으로 비슷하나, 페이지가 리프레쉬된다. 또 입력된 데이터를 서버로 전송.

- fieldset : input태그를 사용하지 않으며. 하나의 입력받을 그룹을 생성한다.
    
    legend 속성 : 범례라는 뜻으로 사용되며, 그룹에 대한 설명을 함.
    
    ![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%2011.png)
    

### HTML5부터 추가된 <input> type속성값

color : 사용자가 직접 색상을 선택하여 입력할 수 있게함.

- date : 사용자가 날짜(년도, 월, 일)을 직접 선택할 수 있음.
    
    min, max 속성 : 사용자가 직접 선택할 수 있는 날짜의 범위를 제한할 수 있다. 지정한 날짜의 아래나 위로는 보이지 않게 됨.
    

time : 사용자가 직접 시간을 선택할 수 있음.

datetime-local : 사용자가 직접 날짜와 시간을 선택할 수 있음.

month : 사용자가 직접 날짜를 선택할 수 있는데, 연도와 월까지만 설정가능.

week : 사용자가 년도를 골라 해당년도의 몇번째 주인지 선택할 수 있다.

- number : 사용자가 숫자를 입력할 수 있다.
    
    min, max 속성 : 이 속성을 추가해 입력할 수 있는 숫자의 제한을 둘 수 있다.
    
- range : 사용자가 슬라이 형식으로 숫자를 입력할 수 있다.
    
    min, max 속성 : 지정하지 않으면 숫자의 시작과 끝이 없어 어느 숫자를 입력했는지 모르나, 이 속성으로 범위를 명시해주면, 숫자를 고를 수 있다.
    

tel : 전화번호를 입력할 수 있다. (safari 8에서만 지원)

email : email주소를 입력받으며, 웹브라우저 지원여부에 따라 유요한 이메일인지 검사해준다.

url : 사용자가 url주소로 입력하게 하며, 웹브라우저 지원여부에 따라 유효한 url주소인지 확인해준다.

search : 사용자가 검색어를 입력할 수 있게하며, text속성값과 비슷해 보이나, 검색어를 지울 수 있는 x표시가 생기는 차이가 있다.

### HTML <Input> 속성들

value 속성 : 입력칸의 초기값을 설정한다.

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%2012.png)

readonly 속성 : 사용자가 입력을 할 수 없게 만드는 상태에다. 주로 value속성의 값으로 데이터를 명시해 읽게만 하고 입력할 수 없는 상태로한다. 그러다 일정 조건이 되면 자바스크립트로 readonly 속성을 제거하는 형식으로 사용된다. 여기서 disabled와 쓰임새가 비슷해 보이나, disabled는 값도 입력할 수 없고, value값이 서버로 전송되지 않는다. 하지만 readonly 속성은 입력할 수는 없어도 value로 명시된 값이 서버로 전송된다. 또, 드래그와 복사가 가능하다.

disabled 속성 : 사용자가 아무것도 할 수 없게 만든다. 입력도 안되고 드래그도 안된다. 서버로 값이 전송되지도 않는다.

maxlength 속성 : 사용자가 입력할 수 있는 문자열의 길이를 설정한다.

size 속성 : 입력창의 크기를 문자열의 크기로 명시한다. 속성값으로 숫자를 받는다.

### HTML5에 새롭게 추가된 input속성들

autocomplete 속성 : 사용자가 입력한 값을 저장해 다시 입력할 때 자동완성 기능을 사용할 수 있게한다. 디폴트 값은 “off”이고 “on”으로 명시해주면 사용가능하다. 하지만 **text, password, color, date, datetime-local, month, week, email, url, tel, search, range 타입 속성값에서만 사용할 수 있다.**

autofocus 속성 : 웹페이지가 열리면 자동으로 autofocus속성이 적용된 입력칸에 입력할 수 있는 상태가 된다.

form 속성 : 일반적으로 form>태그 안에서 input>태그를 명시하는 방식으로 사용되지만 form>태그로 안에서 input>태그를 명시하지 않아도 form속성으로 form>태그의 id를 명시해주면 위치에 상관없이 연결될 수 있다.

formaction 속성 : 기본적으로 사용자가 데이터를 입력하면 form>태그의 action속성에 명시된 주소로 가서 데이터를 처리하게 되지만, formaction속성을 명시해주면 action속성으로 가지 않고 formaction속성으로 명시된 주소로 데이터를 처리한다. (submit타입과 image타입에서만 가능하다.)

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%2013.png)

formmethod 속성 : 위의 formaction 속성과 똑같이 form>태그에 명시된 method속성값으로 데이터를 처리하는게 아닌, formmethod에 명시된 속성값으로 데이터를 처리하게 됨. (마찬가지로 submit, image에서만 사용가능)

formtaget 속성 : form>태크에서 명시된 혹은 디폴트 값의 target속성값을 무시하고 formtarget속성값으로 응답을 받는다.

width, height 속성 : input>의 타입이 image인 경우 가로와 세로를 조절할 수 있다.

min, max 속성 : 입력받을 값의 최솟값과 최댓값을 설정할 수 있다. **number, range, date, time, datetime-local, month, week**타입에서만 가능하다.

multiple 속성 : email, file타입에서 입력받는 데이터의 갯수를 2개이상으로 받을 수 있다.

placeholder 속성 : 입력창에 텍스트를 표시하여 무엇을 입력해야할지 명시해주는 용도이다. 사용자가 입력하면 사라진다.

required 속성 : 이 속성이 명시되면 반드시 입력을 해주어야한다. 입력하지 않고 엔터치면 경고문이 뜸.

step 속성 : 숫자의 간격을 조정한다. **number, range, date, time, datetime-local, month, week** 
타입에서만 사용가능하다.

input>의 각 속성값의 특징

[http://www.tcpschool.com/html/html_input_forms](http://www.tcpschool.com/html/html_input_forms)

[http://www.tcpschool.com/html/html5_element_input](http://www.tcpschool.com/html/html5_element_input)

[http://www.tcpschool.com/html/html5_element_inputtype](http://www.tcpschool.com/html/html5_element_inputtype)

input>의 속성

[http://www.tcpschool.com/html/html5_element_inputattr](http://www.tcpschool.com/html/html5_element_inputattr)

HTML과 CSS

CSS(Cascading Style sheets) html을 어떻게 꾸밀지 정할 수 있는 스타일 시트 언어이다. 

HTML과 JS

자바스크립트(JavaScript)는 HTML로 웹의 틀을 만들고 CSS에서 디자인한 웹 페이지를 동작할 수 있게 만드는 언어이다. Node.js 프레임워크를 사용하면 서버 언어로도 활용할 수 있고, 대부분의 웹 브라우저에서 자바스크립트 인터프리터가 내장되어 있다.

script>태그

script>태그에서는 해당 웹 페이지를 어떻게 동작시킬 건지 정의한다. 직접 태그안에서 정의할 수도 있고 주로는 외부 스크립트파일의 주소를 src속성으로 받아서 사용한다.

HTML과 XHTML

HTML을 사용하는 웹 페이지가 PC의 환경 뿐만 아니라 모바일 등에서도 사용하며 그 활용이 빈번해져 HTML의 자율성이 코드의 해석을 어렵게해서 생기는 문제를 예방하고자 XHTML이 등장했다. XHTML은 HTML과 다르게 엄격한 문법을 요구한다. XHTML을 사용할 시 반드시 <!DOCTYPE>을 통해 명시해주어야함.

HTML5

HTML5는 차세대 표준이다. 문법적으로 매우 유연해졌다. 사용시에는 반드시 !DOCTYPE html>으로 명시해주어야한다.

의미요소(semantic element)

의미요소는 그 자체만으로도 무슨 역할인지 개발자가 알 수 있는 태그들을 말한다. 아닌것으로는 div>, span>등이 있다 이 둘은 직접 코드를 살펴봐야만 그 의미가 명확해지지만, table>같은 태그들은 그 자체만으로도 표를 만드는데 사용되었다는 것을 알 수 있다. 단, 의미만 부여할뿐 따로 기능을 명시하지 않으면, 아무런 동작이 없다.

더 많은 의미요소 >> [http://www.tcpschool.com/html/html5_element_semantic](http://www.tcpschool.com/html/html5_element_semantic)

![Untitled](HTML%2005ff7ff17f934db9b2f21f9104144389/Untitled%2014.png)

### 멀티미디어

HTML5 이전에는 멀티미디어 파일을 지원하는 방식이 복잡했으나, HTML5부터는 멀티미디어 파일의 확장자만으로 그 파일의 type을 결정합니다. ex) 123.mp4 >> 비디오 파일로 인식

type으로 인식되는 확장자 목록 >>[http://www.tcpschool.com/html/html5_multimedia_filetype](http://www.tcpschool.com/html/html5_multimedia_filetype)

video>태그

HTML5에서는 video>태그로 웹페이지에 비디오를 삽입하는 표준화된 방식을 제공한다.

[http://www.tcpschool.com/html/html5_multimedia_video](http://www.tcpschool.com/html/html5_multimedia_video)

audio>태그

HTML5에서는 audio>태그로 웹페이지에 오디오를 삽입하는 표준화된 방식을 제공한다.

[http://www.tcpschool.com/html/html5_multimedia_audio](http://www.tcpschool.com/html/html5_multimedia_audio)

iframe> vs object> vs embed>

3가지 태그 모두 외부 리소스를 웹페이지에서 볼 수 있게 해주는 태그이지만, 주로 유뷰브나 음악 등을 표시할 때는 iframe> pdf파일을 표시할 때는 object>를 사용하는 듯하다. embed는 구식이여서 굳이?인 느낌인 듯 하다…

canvas> 태그 

canvas>태그는 웹 페이지에서 그래픽을 그려주는 태그이다. 구현은 자바스크립트로 한다.

사용법 >>

[http://www.tcpschool.com/html/html5_graphic_canvas](http://www.tcpschool.com/html/html5_graphic_canvas)

svg> 태그

svg> 태그는 canvas>와 같이 그래픽을 그려주는 태그이다. 다른 점은 픽섹로 표현되는 웹페이지에서 벡터(vector)를 표현해 그릴 수 있다. 그렇기 때문에 곡석의 표현이 자유롭고 그래프를 그리는 곳에서 강력한 이점이 있다.

svg> 사용법 >>

[http://www.tcpschool.com/html/html5_graphic_svg](http://www.tcpschool.com/html/html5_graphic_svg)

canvas>와 svg>

둘은 비슷한 기능을 지원하지만 경우에 따라 서로가 가진 이점이 다르다. 

화면이 커지거나 픽셀 수가 늘어나면서(둘은 반대되는 행동, 화면의 크기가 커지면 그래픽 품질이 떨어짐, 픽셀의 수가 늘어나면 그래픽 품질이 올라감) 렌더링의 시간이 달라진다. 화면의 크기가 작을수록, 픽셀의 수가 많아질 수록 벡터로 표현하는 svg>가 렌더링시간에서 이점을 갖는다. 반대의 경우에는 벡터로 표현하는 것이 어려워지기 때문에 canvas>가 이점을 갖는다. 정확한 수치로는 픽셀의 수가 10k이상일 경우 svg>가 이하일 경우 canvas>가 좋다.

더 정확한 비교 >>

[http://www.tcpschool.com/html/html5_graphic_canvasVsSvg](http://www.tcpschool.com/html/html5_graphic_canvasVsSvg)

geolocation API

사용자의 현재 위치 정보를 가져올 때 사용하는 자바스크립트로 된 API

getCurrentPosition() 메소드를 사용해서 사용자의 위도와 경도를 알아낼 수 있다. 사용자가 위치정보 제공 동의를 하지 않으면 사용불가.

geolocation API 메소드와 기능 >>

[http://www.tcpschool.com/html/html5_api_geolocation](http://www.tcpschool.com/html/html5_api_geolocation)

drag and drop API

웹 페이제 내에 요소를 드래그할 수 있는 기능을 제공해주는 API 

drag and drop API 메소드 >>

[http://www.tcpschool.com/html/html5_api_dragAndDrop](http://www.tcpschool.com/html/html5_api_dragAndDrop)

Web Storage API

웹 스토리지 API는 서버에 정보를 저장해서 불러오는 방식이 아닌 사용자의 컴퓨터에 정보를 저장해 언제나 쉽게 가져올 수 있게 하는 기능이다. 이렇게 저장된 정보를 서버로 가지않는다. 이 정보는 같은 출처(origin)라면 그 정보를 공유한다. 

여기서 출처(origin)이란 쉽게 말해 같은 사이트 내에서 페이지를 옮겨도 같은 사이트인 것을 의미함. 다시말해 유튜브에서 동영상을 클릭해서 다른 페이지로 넘어가도 그 페이지도 유튜브인 것이랑 같은 의미이다. 정확한 설명은 >> [https://etloveguitar.tistory.com/83](https://etloveguitar.tistory.com/83)

웹 스토리지 객체에는 크게 두 가지가 있다. 

- sessionStorage 객체
- localStorage 객체

sessionStorage 객체 와 localstorage 객체의 차이점은 정보의 보관에서의 차이이다. sessionStorage는 정보를 저장하고 탭을 닫거나 pc를 종료하면 정보가 사라지지만 localStorage는 탭을 닫거나 pc를 종료해도 지워지지 않는다.

Application Cache API

웹에 필요한 정보를 cache에 저장해서 접근할 수 있게하는 기능이다. cache에 저장하면 사용자의 pc에 저장되는 정보이기 때문에 오프라인으로 접속해도 사용할 수 있고, cache에 이미 저장되어 있기 때문에 load되는 속도가 빠르다. 서버에 정보가 변동되었을 때만 cache를 갱신해주면 된다.

cache에는 3개의 session으로 이루어진다.

- cache mainfest : 정보를 저장해 오프라인에서 쓸 수 있게하고 원할 때마다 갱신가능
- network : 서버와 공유해야하는 파일을 저장하며, 이 파일은 cache에 저장되지 않음.
- fallback : 파일에 접속이 불가능 할 때에 사용할 파일을 저장

cache가 갱신되는 경우 

- 사용자가 저장된 파일을 캐시에서 강제로 지웠을 경우
- cache가 프로그램에 의해 갱신됐을 경우
- cache mainfest에 저장된 파일이 갱신되었을 경우

web worker API

웹 페이지가 실행되면 페이지를 동작시키기 위해 하나의 Thread를 만들어 스크립트를 실행한다. 스크립트를 읽는 것이 끝날 때까지는 다른 동작을 할 수 없는데 이때 web worker는 스크립트를 읽는 Thread 외에 새로운 Thread에서 개별적인 동작을 할 수 있게 해준다.

web worker를 사용하는 큰 틀은 web worker를 사용할 객체를 만들고 함수에서 사용하고 나서 terminate()함수로 동작을 종료 시켜줘야함 web worker는 항상 다음 동작을 이어갈 준비를 하고 있기 때문에 반드시 종료해주어야 함. 마지막으로 undefined 선언으로 마무리 해주어야 재사용할 수 있음.

Server Sent Events API

웹 페이지가 서버로 부터 갱신된 정보를 주기적으로 자동으로 받을 수 있도록 해줌.