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
  - 단위에 주의
  - px(PiXel) 단위 : 가장 단순한 단위
  - dp(Density independent Pixels) 단위 : 안드로이드의 기본 단위(참고. ios의 기본단위는 pt(PoinT))
- 버튼 너비, 높이 실습<br/>
  1. 너비 : wrap_content, 높이 : wrap_content
        ```
        <LinearLayout
            android:layout_width="300dp"
            android:layout_height="300dp"
        >
            <Button
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="너비 : WC 높이 : WC" 
            />
        </LinearLayout>
        ```
        ![wcwc](https://user-images.githubusercontent.com/111935711/201510204-f81aa1cb-f124-45e1-ac25-d4c25816e562.jpg)
    <br/>
    2. 너비 : match_parent, 높이 : wrap_content
        ```
        <LinearLayout
        android:layout_width="300dp"
        android:layout_height="300dp"
        >
        <Button
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="너비 : MP 높이 : WC"
        />
        </LinearLayout>
        ```
        ![mpwc](https://user-images.githubusercontent.com/111935711/201510311-34d37c44-ef76-4428-9006-40c083cde0af.jpg)
    <br/>
    3. 너비 : wrap_content, 높이 : match_parent
        ```
        <LinearLayout
        android:layout_width="300dp"
        android:layout_height="300dp"
        >
        <Button
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:text="너비 : WC 높이 : MP"
        />
        </LinearLayout>
        ```
        ![wcmp](https://user-images.githubusercontent.com/111935711/201510448-e83ae2b6-8c88-4fda-ae15-132464384210.jpg)
    <br/>
    4. 너비 : match_parent, 높이 : match_parent
        ```
        <LinearLayout
        android:layout_width="300dp"
        android:layout_height="300dp"
        >
        <Button
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:text="너비 : MP 높이 : MP"
        />
        </LinearLayout>
        ```
        ![mpmp](https://user-images.githubusercontent.com/111935711/201510519-5f2788d1-e83d-4b56-ac12-a9615e26fedc.jpg)
    <br/>
    5. 너비 : 단위, 높이 : 단위
        ```
        <LinearLayout
        android:layout_width="300dp"
        android:layout_height="300dp"
        >
        <Button
            android:layout_width="200dp"
            android:layout_height="100dp"
            android:text="너비 : 단위(200dp)\n높이 : 단위(100dp)" 
        />
        </LinearLayout>
        ```
        ![단위단위](https://user-images.githubusercontent.com/111935711/201510895-77ded6f7-26e1-4816-8293-0e469eddb83d.jpg)

- background 속성
  - 위젯의 색상을 주로 #RRGGBB 값으로 지정
  - background 속성이 적용되지 않을 때 backgrountTint 속성 사용
  ```
  <LinearLayout
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:background="#0000FF"
  >
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:backgroundTint="#FF0000"
        android:text="Background 실습" 
    />
    </LinearLayout>
  ```
  ![background](https://user-images.githubusercontent.com/111935711/201511925-e550eec1-49f9-475a-85b4-e5153483ca23.jpg)

- padding, layout_margin 속성
  - padding 속성 : 레이아웃 경계선과 위젯 사이에 여백을 둘 수 있음

