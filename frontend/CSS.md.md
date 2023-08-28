# CSS

CSS란?

CSS(Cascading Style sheets) html을 어떻게 꾸밀지 정할 수 있는 스타일 시트 언어이다. 

CSS를 사용하는 이유

HTML에서도 속성값을 사용해 직접 스타일을 지정해 줄 수 있지만 각각의 요소를 일일히 지정해주어야 하고 세부적으로 적용하기 복잡하지만 CSS는 스타일을 파일에 정의하고 이 것을 일괄적이고 편리하게 적용할 수 있게 해준다.

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled.png)

CSS에서 스타일 선언은 크게 선택자(selector)와 선언부(declaratives)로 나뉜다. 선택자는 HTML에 적용시킬 태그를 명시하고, 선언부에는 스타일 내용을 {}으로 표시하여 적는다. 속성과 속성값은 콜론(:)으로 구분한다. 선언부 안에서 각 속성은 세미콜론(;)으로 구분하고 마친다.

주석은 /* 내용 */으로 C와 같다. 단, 주석 안에 주석기호를 또 넣으면 안된다.

CSS 적용 방법에는 3가지가 있다.

1. 인라인 스타일(Inline style)
2. 내부 스타일 시트(Internal style sheet)
3. 외부 스타일 시트(External style sheet)

인라인 스타일(Inline style)은 태그의 속성 style에서 속성값을 직접 지정하는 방법인데 오직 그 태그에서만 적용된다.

내부 스타일 시트(Internal style sheet)는 <head>태그 안에서 <style>태그 안에서 정의해서 적용하는 방식이다. 단, 해당 html문서에서만 적용가능하다.

외부 스타일 시트(External style sheet)는 따로 css파일 안에서 정의해서 <head>태그에서 <link>태그로 css파일을 불러와서 적용할 수 있게 해준다. css파일에서 한 번 정의하고 필요할 때마다 불러올 수 있기 때문에 주로 사용할 듯하다.

ex) <link rel=”stylesheet” type=”text/css” href=”파일명”>

### CSS 적용 우선 순위

- importance : 선언부에 속성값 뒤에 !importance를 적고 ;로 마무리하면 다른 것 보다 가장 우선순위가 된다.
- specificity: 따로 importance를 표시하지 않았다면 다음과 같은 순서로 적용된다. 또한 모든 설정이 같을 경우 가장 나중에 적용된 시트를 적용한다. 예를 들어 같은 태그에 다른 스타일이 외부에 정의 되었다면 가장 나중에 정의한 태그가 적용된다.
    1. 인라인 스타일 시트
    2. 외부 또는 내부 스타일 시트 (id 선택자 > class 선택자 > tag 선택자)
    3. 브라우저 기본 값(디폴트 값)

선택자(selector) css를 적용시키기 위해 사용하는 방법이다.

- 전체 선택자
- HTML 요소 선택자
- 아이디(id) 선택자
- 클래스(class) 선택자
- 그룹(group) 선택자

전체 선택자

적용대상을 html 문서 전체로한다. 

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%201.png)

HTML tag 선택자

CSS적용 대상을 태그이름으로 하여 해당태그는 모두 적용시키는 방법이다.

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%202.png)

아이디(id) 선택자

아이디 이름에 스타일을 적용시켜 사용한다. html과 css에서는 하나의 웹페이지에서 하나의 아이디가 중복되어도 문제가 없지만, 이 문서로 자바스크립트를 적용시킬때에는 오류가 생길 확률이 높다. 그렇기 때문에 아이디를 선택자로 활용하는 것 보단 클래스를 선택하는게 좋다. #문자와 id명을 적어 정의한다.

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%203.png)

클래스(class) 선택자

아이디 선택자와 같이 같은 클래스 이름을 적용한 태그에서 모두 적용한다. 

.문자와 class이름으로 정의한다.

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%204.png)

그룹 선택자

그룹 선택자는 같은 스타일이 중복될 때 쉼표(,)로 구분하여 한 번에 여러 선택자들에 같은 스타일을 적용될 수 있게 해준다.

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%205.png)

결합 선택자

결합 선택자는 선택자들 간의 관계를 설정함.

자손 선택자(descendant selector)

자손 선택자는 해당 태그의 하위 요소를 지정해서 해당 하위요소 모두 스타일을 적요한다. 밑의 예와 같이 <div>의 <p>태그는 모두 스타일의 영향을 받는다고 할 수 있다.

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%206.png)

자식 선택자(child selector)

자식 선택자는 해당 태그의 바로 아래 태그에만 영향을 미친다. 즉, 자손 선택자와는 다르게 해당 태그의 바로 아래 태그가 아닌 아래아래(?) 태그에는 영향을 미치지 않는다.

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%207.png)

동의 선택자

[http://www.tcpschool.com/css/css_selector_sibling](http://www.tcpschool.com/css/css_selector_sibling)

## CSS 색

### CSS에서 색을 표현하는 방법

1. 색상 이름으로 표현 : aqua, black, blue, fuchsia 등등… 140개의 색상을 이름으로 표현
2. RGB 색상값으로 표현 : R(red), G(green),B(blue) 각 값을 수치로 정해 하나의 색을 지정함.
3. 16진수 색상값으로 표현 : RGB로 표현한 색상값을 16진수로 표현된 숫자랑 매치해서 색상을 표현

### CSS에서 색상 속성

- 배경색 지정
    - background-color : 색상명;
        
        background-color : 색상명;은 해당 선택자의 배경색을 설정
        
        background-img : url(”이미지 주소”);은 선택자의 배경 이미지를 설정. 디폴트 값은 가로방향 세로방향으로 이미지 반복. 아래 선언을 추가해서 반복을 제어할 수 있음.
        
        - background-repeat : repeat-x; >> 가로방향으로 반복
        - background-repeat : repeat-y; >> 세로방향으로 반복
        - background-repeat : no-repeat; >> 반복하지 않음.
        
        background-position : (왼쪽여백)px (위쪽여백)px; >> 지정한 픽셀 값만큼 여백을 두어 배경 이미지를 표기
        
        위의 요소를 전부 합해서 표기할 수 있다.
        
        >> background: url(”이미지 주소”) no-repeat 20px 20px;
        
        >> 이미지를 배경으로하고 반복하지 않고, 왼쪽 20px 상단 20px떨어져서 이미지 표시.
        
- 경게선 색상 지정
    - border : 1px solid 색상명;
        
        크게 3개를 설정할 수 있음.
        
        - 선 모양: style
            - 경계선 위쪽 모양(style) 지정 : border-top-style
            - 경계선 아래쪽 모양(style) 지정 : border-bottom-style
            - 경계선 왼쪽 모양(style) 지정 : border-left-style
            - 경계선 오른쪽 모양(style) 지정 : border-right-style
            - 경계선 한꺼번에 모양(style) 지정 : border-style
                
                한꺼번에 적용시 하나의 스타일을 주면 전부 같은 스타일로 표시되고, 위,우,아래,좌 순으로 표시할 수도 있음.
                
                - none : 기본값(모양 없음)
                - hidden : 경계선 숨김
                - solid : 실선
                - double : 두줄
                - groove : 선이 안쪽으로 들어간 느낌
                - ridge : 선이 바깥으로 튀어나온 느낌
                - inset : 내용이 안으로 들어간 느낌
                - outset : 내용이 밖으로 나온 느낌
                - dashed : 긴 점선
                - dotted : 짧은 점선
        - 선 두께: width
            - 경계선 위쪽 두께(style) 지정 : border-top-width
            - 경계선 아래쪽 두께(style) 지정 : border-bottom-width
            - 경계선 왼쪽 두께(style) 지정 : border-left-width
            - 경계선 오른쪽 두께(style) 지정 : border-right-width
            - 경계선 한꺼번에 두께(style) 지정 : border-width
            
            반드시 border-style과 함께 사용하여야 한다.
            
            - thin, medium, thick
            - px, pt, em
            
            으로 두께 조절
            
            한꺼번에 적용하는 법은 다른 설정과 같음.
            
        - 선 색상: color
            - 경계선 위쪽 색깔(color) 지정 : border-top-color
            - 경계선 아래쪽 색깔(color) 지정 : border-bottom-color
            - 경계선 왼쪽 색깔(color) 지정 : border-left-color
            - 경계선 오른쪽 색깔(color) 지정 : border-right-color
            - 경계선 한꺼번에 색깔(color)지정 : border-color
            
            반드시 border-style과 함께 사용해야 함.
            
            - color : 색상명;
            - color : rgb(255, 99 ,71);
            - color : #ff6347;
            - color : hsl(9, 100%, 64%);
            - color : rgba(255, 99 ,71, 0.6);
            
            한꺼번에 적용하는 법은 다른 설정과 같음.
            
        
        위의 설명처럼 border : 두께 모양 색상;으로 한번에 정의할 수 있음. 또한 border-top처럼 한 부분만 떼어서 전부 지정할 수 있음.
        
        - 둥근 경계선
            - border-radius : 10px; 처럼 써서 둥근 경계선을 두께를 설정해서 표시할 수 있음.
- 글자 색상 지정
    
    color : 색상명;
    
- 색상 값 표기
    
    color : 색상명;
    
    color : rgb(값, 값, 값);
    
    color : #ff6347(16진수)
    
    color : hsl(색상, 채도, 명도)
    
    색상: 0 ~ 360의 값으로 색 선택. 색상환의 각도를 나타냄. (0 = red, 120 = green, 240 = blue)
    
    채도: 0~100%의 값을 적음. 숫자가 작아질 수록 어두움. 100%는 컬러 최대치 (표기시 %필수)
    
    명도: 0~100%값을 표시, 작을 수록 검은색을 뜀 높을 수록 흰색으로. (%필수)
    
    color : rgba(r, g, b, 투명도);
    
    rgb표기에서 투명도를 넣은 표기법. 투명도는 0.0 ~ 1.0사이값으로 표기함.
    

### 박스 모델

HTML도 크게 보면 박스모델이다. 그리고 CSS에서 디자인이나 레이아웃을 말할 때도 사용된다.

- Margin : 경계선으로부터 바깥 여백
- Border : 경계선
- Padding : 경계선으로부터 안쪽 여백
- Content : 사용자에게 보여지는 내용

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%208.png)

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%209.png)

![Untitled](CSS%20a8fd1f4827254a85b87c7a43c9b7152a/Untitled%2010.png)

padding과 margin은 top,right,bottom,left, 한꺼번에 으로 지정하여 스타일을 지정할 수 있고, 한꺼번에 지정할 때 하나의 스타일을 지정하거나, 상,우,아래,좌 순으로 배치, (위아래) (좌우)로 분류하여 지정, (위) (좌우) (아래)로 분류하여 지정가능.

content의 크기를 width(가로), height(세로)로 지정하여 표기할 수 있음. 또 max-를 붙여 최대값, min-을 붙여 최소값을 지정할 수 있음. 

px는 모니터의 크기에 상대적인 크기를 가지고, %는 브라우저 폭에 대한 상대적 크기를 가짐.

### font

- 글꼴 지정
    - font-family : 글꼴명;
- 글자크기 지정
    - font-size : 크기(숫자+단위);
- 글꼴 스타일
    - font-style : normal, italic;
- 글꼴 굵기
    - font-weight : normal, bold;
- 글자간격 지정
    - letter-spacing : 숫자px;
- 글자 색상 지정
    - color : 색상명 ;
- 글자꾸밈효과 지정
    - text-decoration : none, underline, line-through, overline

### Text

- 가로방향 정렬
    - text-align : left, center, right;
- 세로방향 정렬
    - vertical-align : top, middle, bottom;
- 들여쓰기
    - text-indent : 숫자px;
- 줄 간격
    - line-height : 숫자px;
- 줄바꿈 방지
    - white-space : normal, nowrap;
- 대소문자 설정
    - text-transform : uppercase, lowercase, capitalize;

### link

- a : link { } : 한번도 방문한적 없는 상태(디폴트 값).
- a : visited { } : 한번이라도 방문한 상태.
- a : active { } : 링크를 마우스로 누른 상태
- a : hover { } : 링크위에 마우스를 올려놓은 상태

선언부에서 세부 스타일을 지정해서 각 링크의 상태에서의 스타일을 지정할 수 있음.

### list

- 항목(글머리) 기호 지정
- 항목 이미지 지정
    - list-style-image : url('이미지 주소');

background 속성들 >> [tcpschool.com/css/css_basic_backgrounds](http://tcpschool.com/css/css_basic_backgrounds)

text 속성들 >> [http://www.tcpschool.com/css/css_basic_text](http://www.tcpschool.com/css/css_basic_text)

font 속성들 >> [http://www.tcpschool.com/css/css_basic_fonts](http://www.tcpschool.com/css/css_basic_fonts)

link 속성들 >> [http://www.tcpschool.com/css/css_basic_links](http://www.tcpschool.com/css/css_basic_links)

list 속성들 >> [http://www.tcpschool.com/css/css_basic_lists](http://www.tcpschool.com/css/css_basic_lists)

table 속성들 >> [http://www.tcpschool.com/css/css_basic_tables](http://www.tcpschool.com/css/css_basic_tables)

### Position

CSS로 문서상에서 레이아웃을 표시할 위치를 정할 때 position속성을 활용한다. top, bottom, left, right속성을 추가해서 위치를 조정한다.

- static : static은 디폴트 값으로 상하좌우 위치를 지정해도 영향을 받지않고 본래 위치(position의 속성의 영향을 받지않고, html에서 지정해준 위치)로 지정된다.
- relative : 상하좌우를 지정해준 위치를 본래위치를 기준으로 이동함.
- absolute : 부모(html 문서상 자신을 감싸고 있는 태그 중 가장 가까운 태그이면서 position이 static이 아닌 태그)태그를 기준으로 상하좌우 지정한 위치로 이동. 만약 부모태그가 없다면 <body>를 기준으로 삼음. 다른 속성과 달리 absolute를 할당하면 해당 요소가 차지하는 공간을 없애고 다른 요소와 겹치게됨.
- fixed : 뷰포터를 기준으로 삼아 스크롤을 하고 화면 크기를 바꿔도 브라우저에서 지정된 위치에서 벗어나지 않음. 예를 들어 사이트의 팝업광고를 보면 스크롤을 해도 화면을 키워도 위치가 변하지 않음.

### 레이아웃 순서지정

레이아웃을 지정하다 보면 서로 겹치는 경우가 생길 수도 있다. 그래서 순서를 지정해 줘서 어떤 레이아웃이 가장 바깥으로 표시될 지 정할 수 있다.

- z-index : 숫자(정수) : 숫자가 높을 수록 바깥에 표시된다. 반대로 낮을 수록 가장 뒤로 위치한다. 반드시 position관 함께 사용해야한다.
- visibility 속성 : 레이아웃을 보이게(디폴트)하거나 보이지 않게 할 수 있다.
    - visibility : hidden; : 해당 레이아웃이 인터페이스 상에서 보이지 않는 상태이다. 하지만, 보이지만 않을 뿐 해당 공간을 차지하고 있는 상태이다.
    - visibility : visible; : 디폴트 값으로 사실상 의미가 없다.

### 레이아웃 너비지정

- width : `width` 속성은 브라우저 너비까지 커지는 것을 막을 수 있다.
- max-width : 최대 너비를 지정하고, 해당 너비 이하는 브라우저 너비에 맞춘다.
- auto : width와 함께 사용시, 해당 요소를 수평적으로 중앙에 위치시킨다.

### display 속성

display속성은 inline형태를 block으로 block을 inline으로 바꾸고 싶을 때 사용할 수 있다.

- none : 화면상에서 보이지 않게 한다는 점에서 visibility : hidden과 같지만, visibility : hidden은 화면상으로만 보이지 않지 실제 해당 공간을 차지한다. 하지만 none은 해당 공간을 차지하지도 않고, 원래 없었던 것처럼 표현된다.
- inline : 필요한 폭만 가진다
- block : 새 줄에서 시작하며 브라우저 전체 폭을 차지한다

CSS 이미지 스프라이트

웹 페이지가 실행되면 서버에 필요한 파일을 요청한다. 그 중에는 이미지도 있는데 만약 요청해야하는 이미지의 수가 많다면 그 만큼 웹 페이지를 로딩하는데 걸리는 시간이 길어진다. 이 것을 해결하기 위해 이미지 스프라이트(Image Sprite)는 이미지를 하나의 파일로 합쳐 단 몇번만의 요청으로도 필요한 이미지를 다 받고 다시 쪼개서 사용한다. 단, 다양한 이미지를 합치는 것은 오히려 효율이 떨어질 수 있다. 그렇기 때문에 비슷하거나 용도가 유사한 이미지끼리 묶어서 합치지는게 좋다.

animaition 기능을 사용해 역동적인 이미지를 표현할 수도 있다.

CSS 크기 단위

CSS에서 사용하는 크기 단위는 %, em, px, cm, mm, inch 등이 있으나 주로 사용하는 단위는 아래와 같다.

1. 백분율 단위(%) : 표준을 100%로 하고 그 상대적인 크기로 조절한다.

2. 배수 단위(em) : 표준을 1em으로 하고, 상대적으로 적용한다. font에서 잘 사용됨.

3. 픽셀 단위(px) : 픽셀의 수를 절대적인 것으로 정의하고 크기를 정함.

CSS 크기 속성들 >> [http://www.tcpschool.com/css/css_boxmodel_dimension](http://www.tcpschool.com/css/css_boxmodel_dimension)