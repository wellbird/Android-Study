# Chapter4. 기본 위젯 익히기
## 뷰의 개요
### 뷰와 뷰그룹
-----
- 뷰(View) 클래스
  - 안드로이드 화면에서 실제로 사용되는 것들은 모두 View 클래스의 상속을 받음
  - "위젯"이라고도 부름

- 레이아웃
  - 다른 위젯을 담을 수 있는 위젯을 특별히 레이아웃이라고 함
  - ViewGroup 클래스 아래에 존재

### 안드로이드에서의 위젯
-----
  ![위젯과레이아웃](https://user-images.githubusercontent.com/111935711/201508622-f2bff7e0-8115-46f2-bbcf-f0071db63919.jpg)

### View 클래스 계층도
-----
  ![View클래스계층도](https://user-images.githubusercontent.com/111935711/201508686-2cc41a20-e602-4f45-b76f-eb554adadad6.jpg)
- 최상위에 Object(java.lang.Object) 클래스가 있고 이를 상속받는 View 클래스가 있음
- 안드로이드 화면에 나타나는 못든 위젯은 View 하위에 존재
- 뷰 컨테이너(View Containder) : 레이아웃이라고 부르지는 않지만 다른 뷰를 포함(ex. ListView, GridView, etc...)

### 버튼의 속성
-----
- XML 속성이 거의 없고 대부분 상위 클래스인 TextView나 View에서 상속받음
- https://developer.android.com/reference/packages 에서 속성 확인
  ![클래스의상속관계를찾는방법](https://user-images.githubusercontent.com/111935711/201509025-d4ba9acb-2ebe-45ef-8658-8530d6a61724.jpg)

## View 클래스의 XML 속성
### View 클래스의 주요 XML 속성
-----
- View 클래스가 모든 위젯의 부모 - 위젯과 레이아웃 등은 모두 View 클래스의 속성과 메소드를 상속받음
- View 클래스의 속성을 파악하면 하위 클래스도 쉽게 이해할 수 있음

### id 속성
-----
- 모든 위젯의 아이디를 나타냄
- Kotlin 코드에서 버튼 등의 위젯에 접근할 때 id 속성에 지정한 아이디를 사용
- 일반적으로 id 속성은 위젯에 아이디를 새로 부여하는 개념
  - '@ + id/'형식
    - / 다음에는 새로 지정할 id를 넣음
    - ex) android:id = "@+id/btn1" : 버튼 위젯의 아이디로 btn1을 부여
  - 접근방식
  ```
  위젯 변수 = findViewById<위젯형>(R.id.위젯id)
  ```
  ```
  var button1 : Button
  button1 = findViewById<Button>(R.id.button1)
  ```

- 터치했을 때 어떤 동작이 필요한 경우 id 지정
  ![id속성의xml코드](https://user-images.githubusercontent.com/111935711/201509743-a474fe1d-a678-4657-8dfc-5eff7c7287cd.jpg)

- layout_width, layout_height 속성
  - 모든 위젯에 필수로 들어감
  - 높이와 너비를 표현 - match_parent와 wrap_content 값으로 설정 가능
  - wrap_content : 버튼의 너비가 그 안의 글자에 꼭 맞는 크기가 됨
  - match_parent : 버튼을 싸고있는 부모(LinearLayout)에 꽉 차는 크기가 됨

- 값을 숫자로 직접 지정하는 경우
  - **단위에 주의**
  - px(PiXel) 단위 : 가장 단순한 단위
  - dp(Density independent Pixels) 단위 : 안드로이드의 기본 단위(참고. ios의 기본단위는 pt(PoinT))

### background 속성
-----
- 위젯의 색상을 주로 #RRGGBB 값으로 지정
- background 속성이 적용되지 않을 때 backgrountTint 속성 사용

### padding, layout_margin 속성
-----
- padding 속성 : 레이아웃 경계선과 위젯 사이에 여백을 둘 수 있음
- layout_margin 속성 : 위젯과 위젯 사이에 여유를 둘 수 있음

### visibility 속성
- 위젯을 보일 것인지 여부를 결정
  - visible : 디폴트 값으로 보이는 상태
  - invisible : 안보이는 상태지만, 보이지 않을 뿐 원래의 자리를 유지함
  - gone : 안보이는 상태이며, 원래의 자리까지 사라짐

### enabled, clickable 속성
- XML보다 Kotlin 코드에서 주로 사용
- boolean값을 가지며 디폴트 값은 true
- enabled : 위젯의 동작 여부
- clickable : 클릭이나 터치가 동작 여부

### rotation 속성
- 위젯을 회전시켜서 출력
- 값은 각도로 지정

## 텍스트뷰
- View 클래스 바로 다음에 위치하며 다양한 위젯이 그 하위에 존재

### Text속성
-----
- 텍스트뷰에 나타나는 문자열을 표현
- "문자열"형식으로 값을 직접 입력하거나 "@string/변수명"형식으로 지정한 후 strings.xml 파일에 지정할 수 있음

### textColor 속성
-----
- 글자의 색상을 지정
- background 속성처럼 값은 #RRGGBB나  #AARRGGBB형식을 사용

### textSize 속성
-----
- 글자의 크기를 dp, px, mm, sp단위로 지정

### typeface 속성
-----
- 글자의 글꼴을 지정
- 값으로 sans, serif, monospace를 설정할 수 있고 디폴트는 normal

### textStyle 속성
-----
- 글자의 스타일을 지정
- 값으로 bold, italic, bold|italic을 설정할 수 있고 디폴트는 normal

### singleLine 속성
-----
- 글이 길어 줄이 넘어갈 경우 강제로 한 줄 까지만 출력하고 문자열의 맨 뒤에 "..."을 표시
- 값으로 true와 false를 설정하 수 있고 디폴트는 false

## Kotlin 코드로 XML 속성 설정
### activity_main.xml 파일에서 지정한 XML 속성을 Kotlin 코드에서 설정하는 방법
-----
- Kotlin 코드를 다음과 같이 설정하여 화면에 적용
  ![kotlinToXML](https://user-images.githubusercontent.com/111935711/203701696-2f48cdb9-12fe-4a3d-930a-73cd28dedf25.jpg)

- 많이 사용되는 View 클래스 또는 TextView 클래스의 XML 속성과 메소드
  |**XML 속성**|**관련메소드**|**비고**|
  |:--:|:------:|:------:|
  |background|setBackgroundColor()|View 클래스|
  |clickable|setClickable()|View 클래스|
  |focusable|setFocusable()|View 클래스|
  |id|setId()|View 클래스|
  |longClickable|setLongClickable()|View 클래스|
  |padding|setPadding()|View 클래스|
  |rotation|setRotation()|View 클래스|
  |scaleX, scaleY|setScaleX(), setScaleY()|View 클래스|
  |visibility|setVisibility()|View 클래스|
  |gravity|setGravity()|TextView 클래스|
  |inputType|setRawInputType()|TextView 클래스|
  |password|setTransformationMethod()|TextView 클래스|
  |text|setText()|TextView 클래스|
  |textColor|setTextColor()|TextView 클래스|
  |textSize|setTextSize()|TextView 클래스|

## 버튼과 에디트텍스트
- 버튼과 에디트텍스트는 사용자에게서 어떤 값을 입력받기 위한 가장 기본적인 위젯
- 두 위젯은 View 클래스와 TextView클래스를 상속받으므로 비슷하게 사용 가능
- 필요시 TextView의 하위 클래스인 EditText, RadioButton, CheckBox, ToggleButton 등으로 바꿈

### 버튼
-----
- 버튼을 클릭하는 이벤트를 가장 많이 사용
- 버튼을 클릭했을 대 동작하는 Kotlin 코드를 세 단계로 작성
  1. 버튼 변수 선언 
    ```
    var mybutton : Button
    ```
  2. 변수에 버튼 위젯 대입
    ```
    mubutton = findViewById<Button>(R.id.button1)
    ```
  3. 버튼을 클릭할 때 동작하는 람다식 정의
    ```
    mybutton.setOnClickListener{동작 내용}
    ```
- 세 단계는 대부분의 위젯(라디오버튼, 이미지버튼, 체크박스, 토글버튼 등)에서 거의 동일하게 사용

### 에디트텍스트
-----
- 값을 입력받은 후 해당 값을 Kotlin 코드에서 가져와 사용하는 용도로 많이 쓰임
- 에디트텍스트도 변수를 선언하고 이 변수에 해당 id 값을 넣은 후에 접근함
  1. 에디트텍스트 변수 선언
    ```
    var myEdit : EditText
    ```
  2. 변수에 에디트텍스트 위젯 대입
    ```
    myEdit = findViewById<EditText>(R.id.edittext)
    ```
  3. 에디트텍스트에 입력된 값 가져오기(주로 버튼 클릭 이벤트 람다식 안에 넣음)
    ```
    var myStr : String = myEdit.getText().toString()
    ```

## 컴파운드 버튼
- CompoundButton 클래스
- Button 클래스의 하위 클래스로 체크박스, 라디오버튼, 스위치, 토글버튼의 상위 클래스
- 이 네가지는 공통적으로 체크 또는 언체크 상태가 될 수 있음(실제로 비슷한 형태를 띠지만 용도는 조금씩 다름)

### 체크박스
-----
- 체크박스는 클릭할 때마다 상태가 체크, 언체크로 바뀜
- 여러 개의 체크박스가 있어도 서로 독립적으로 동작한다는 특징이 있어 여러 개를 동시에 체크할 수 있음
- 체크와 언체크가 바뀌었을 때 Kotlin 코드의 처리 절차
  1. 체크박스 변수 선언
    ```
    var mycheck : CheckBox
    ```
  2. 변수에 체크박스 위젯 대입
    ```
    mycheck = findViewById<CheckBox>(R.id.android)
    ```
  3. 체크박스가 변경될 때 동작하는 람다식 정의
    ```
    mycheck.setOnCheckedChangeListner{compoundButton, b -> 동작내용}
    ```

### 스위치와 토글버튼
-----
- 스위치와 토글버튼은 모양만 조금 다를 뿐 용도는 거의 동일함
- 스위치의 주 용도는 온/오프 상태 표시
  - XML 속성이나 관련 메소드는 모두 체크박스와 동일하게 사용 가능
  - checked 속성은 true와 false에 따라서 색상과 글자가 다르게 표현

### 라디오버튼과 라디오그룹
-----
- 라디오버튼
  - XML속성이나 메소드가 체크박스와 거의 동일하지만 용도가 다름
  - 여러 개 중 하나만 선택해야 하는 경우에 사용
    - 라디오 그룹과 함께 사용
    - 각 라디오버튼의 id 속성이 꼭 있어야 함(id속성이 없으면 해당 라디오버튼이 계속 선택된 것으로 지정되어 해제되지 않음)

- 라디오그룹
  - ViewGroup-LinearLayout의 하위 클래스로 존재
  - TextView 하위의 위젯들과는 성격이 조금 다름
  - clearCheck() : 해당 라디오그룹 안에 체크된 것을 모두 해제하는 메소드

### 이미지 뷰
-----
- 그림을 출력하는 위젯
- 그림을 넣거나 화면을 화려하게 구성할 때 사용
  - 그림 파일은 일반적으로 프로젝트의 [res] - [drawable]폴더에 있어야 함
  - 접근은 XML에서 "@drawable/그림id" 형식으로 함
- 이미지뷰와 이미지 버튼의 XML속성
  - src : 이미지의 경로를 나타냄
  - maxHeight/maxWidth : 이미지의 크기를 지정함
  - scaleType : 이미지의 확대/축소 방식을 지정(matrix, fitXY, fitStart, fitEnd, center 등 지정한 값에 따라 이미지를 확대/축소하는 방식이 결정)

# Chapter5. 레이아웃 익히기
## 레이아웃의 개요
### 레이아웃의 기본 개념
-----
- 레이아웃의 대표적인 속성
