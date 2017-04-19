# CHAPTER 2. 데이터: 텍스트와 숫자 다루기

## 2.1 텍스트

#### 문자열(string)
  - 컴퓨터 프로그램에서 사용하는 텍스트 조각  
  - 줄줄이 이어진 개별 요소들로 구성  
    (글자, 숫자, 마침표, 공백 탭 등 어떠한 문자라도 들어갈 수 있음)  
  - 문자열의 최대 길이는 컴퓨터의 메모리 크기로 제한

### 2.1.1 텍스트 문자열 정의

#### 문자열을 나타내는 방법

- **작은따옴표('text')**  
    작은따옴표(')와 역슬래시(\\) 이외 문자는 그대로 취급   

```
print '오늘 저녁 뭐먹을까요?';
print '치킨';
print '032153';
print '"순살"이 좋겠네요';
----------------------------------------------------------------
오늘 저녁 뭐먹을까요?치킨032153"순살"이 좋겠네요
```

- **이스케이프 문자(\\)**   

```
print 'It\'s a piece of cake.';
----------------------------------------------------------------
It's a piece of cake.
```


- **큰따옴표("text")**  
  \- 큰따옴표 문자열 내 포함된 변수명은 해당 변수의 **값**으로 대치  
  \- 큰따옴표 문자열에서 사용할 수 있는 특수 문자  

```
\n           줄바꿈(ASCII 10)
\r           캐리지 리턴(ASCII 13)
\t           탭(ASCII 9)
\\           \
\$           $
\"           "
\0 ~ \\777   8진수
\x0 ~ \\xFF  16진수
```

- **heredoc**  
  \- 큰따옴표 문자열과 같은 이스케이프 문자 사용법과 변수 치환 규칙  

```js
print <<<HEREDOC
<html>
    <head>
        <title>title here</title>
    </head>
    <body bgcolor="#fffed9">
        <h1>dinner</h1>
        Dinner at
        <ul>
            <li>$restorant1</li>
            <li>$restorant2</li>
            <li>$restorant3</li>
        </ul>
    </body>
</html>
HEREDOC;
```

### 2.1.2 텍스트 다루기
문자열 관련 내장함수 중 유효성 검사와 형식화에 유용한 함수

#### 문자열 유효성 검사
우편번호, 이메일 등 제출된 폼 데이터의 유효성 검사

|함수명|기능|사용|
|---|---|---|
|**trim()**|문자열의 시작과 끝에 존재하는 화이트스페이스 제거|trim("   text  ") &rarr; text |
|**strlen()**|문자열의 길이 반환|strlen(" text ") &rarr; 6|
|**strcasecmp()**|대소문자 구분없이 문자열 비교(내용이 같으면 0 반환)|strcasecmp("text", "TExt") &rarr; 0|

#### 텍스트 형식화
- 문자열을 특정 형식으로 출력  

|함수명|기능|사용|
|---|---|---|
| **printf()** |패딩 문자|printf("우편번호 : %05d.", "521")<br> &rarr; 우편번호 : 00521|
||기호|printf("2016년 최저기온 %+d℃ 최고기온 %+d℃ ", -18.0, 36.6)<br> &rarr; 2016년 최저기온 -18℃ 최고기온 +36℃|
||최소 너비|printf("Alphabet : %8s", "ABCD")<br> &rarr; Alphabet :     &nbsp;&nbsp;&nbsp;&nbsp;ABCD<br>printf("Numbers : %05d", "123")<br> &rarr; Numbers : 00123|
||마침표와 정밀도|printf("PI = %.2f", 3.141592) &rarr; PI = 3.14|
| **strtolower()** |문자열 전체를 소문자로 변경  |ex) strtolower("Text")<br> &rarr; text |
| **strtoupper()** |문자열 전체를 대문자로 변경  | strtoupper("Text")<br> &rarr; TEXT |
|**ucwords()**  |문자열 내 각 단어의 첫 글자를 대문자로 변경  | ucwords("text")<br> &rarr; Text |
| **substr()**  |문자열의 일부를 원하는 대로 추출(문자열, 시작위치, 추출할 바이트 수)  | substr("substr test text", 3, 10)<br> &rarr; str test t |
| **str_replace()**  |문자열의 일부를 새로운 문자열로 변경(문자열, 대상 문자열, 새로운 문자열)  | substr("substr test text", "test", "sample")<br> &rarr; substr sample text |


## 2.2 숫자


### 2.2.1 다양한 수 다루기

- 정수  
\- 소수점 이하의 수를 포함하지 않음  
- 부동소수점 수  
\- 소수점 이하의 수가 포함된 수  
\- 소수점의 위치가 고정되어 있지 않고 정밀도에 따라 결정
- 운영체제에 따라 프로그램에서 다룰 수 있는 수의 최대값, 최소값, 소수점 이하 최대 자릿수가 상이함

### 2.2.2 산술 연산자
- \+ : 덧셈
- \- : 뺄셈
- / : 나눗셈
- \* : 곱셈
- ** : 거듭제곱 ( PHP 5.6 이전 버전에서는 pow() 함수 사용 )
- % : 나머지 ( 7 % 3 &rarr; 1 )
- 연산 우선순위는 일반적인 수학 계산 순서를 따름 (곱셉, 나눗셈이 덧셈 뺄셈보다 높음)  
- 모호한 순서는 괄호를 이용해 확실히 한다.

## 2.3 변수

#### 변수  
- 프로그램 실행 과정에서 사용되는 데이터를 담는다  
- 표기 : $variable, $number1, $productCode, $user\_name  
- 할당 : $number1 = 253; $productCode = "TA03920"  
- 변수명 규칙  
  \- 영문 대/소문자(A-Z, a-z), 숫자(0~9), 밑줄문자(\_)  
  \- 인코딩이 UTF-8인 경우 기본 라틴 문자가 아닌 문자(α, β, ┘ 등)도 허용  
  \- <u>대부분 영문 대/소문자, 숫자, 밑줄문자로만 이루어진 변수명을 사용, 대/소문자 구별</u>


### 2.3.1 변수의 연산

- 변수 사용 예제  

```js
$price = 3.93;
$tax_rate = 0.08;
$tax_amount = $price * $tax_rate;
$total_cost = $price + $tax_amount;

$username = 'james';
$domain = '@example.com';
$email_address = $username . $domain;

print '세금은 ' . $tax_amount;
print "\n"; //next line
print '총 가격은 ' .$total_cost;
print "\n"; //next line
print $email_address;

----------------------------------------------------------------

세금은 0.3144
총 가격은 4.2444
james@example.com
```

- 할당과 덧셈 조합

```js
$price = $price + 3;
$price += 3;
```

- 할당과 결합 연산자 조합  

```js
$username = $username . $domain;
$username .= $domain;
```

- 증가와 감소  

```
$birthday = $birthday + 1;
++$birthday;
$years_left = $years_left - 1;
--$years_left;
```

### 2.3.2 문자열 내부에 변수 넣기

변수의 값을 다른 텍스트와 조합해 출력해야 할 경우, 큰따옴표 문자열과 here 문서를 이용

- 변수 삽입 (큰따옴표 문자열)

```js
$email = 'jacob@example.com';
print "reply to $email";
----------------------------------------------------------------
reply to jacob@example.com
```

- here 문서에 변수 넣기

```js
$page_title = '메뉴';
$meat = '돼지고기';
$vegetable = '숙주나물';
print <<<MENU
<html>
    <head><title>$page_title</title></head>
    <body>
        <ul>
            <li>{$meat} 바베큐</li>
            <li>훈제 $meat</li>
            <li>$meat 조림과 $vagetable</li>
        </ul>
    </body>
</html>
MENU;
----------------------------------------------------------------
<html>
    <head><title>메뉴</title></head>
    <body>
        <ul>
            <li>돼지고기 바베큐</li>
            <li>훈제 돼지고기</li>
            <li>돼지고기 조림과 숙주나물</li>
        </ul>
    </body>
</html>
```

- 중괄호로 변수 감싸기  
변수명이 끝나는 위치와 문자열 그대로 출력할 위치를 정확히 지정하기 위해 중괄호 사용 (4장에서 자세히)

```js
$preparation = '삶';
$meat = '소고기';
print "야채를 곁들인 {$preparation}은 $meat"
----------------------------------------------------------------
야채를 곁들인 삶은 소고기
```

## 2.4 마치며

- 프로그램에서 문자열을 정의하는 세 가지 방법 : 작은따움표('text'), 큰따옴표("text"), here 문서(<<&lt;EOT text EOT)
- 이스케이프문자(\\)
- 문자열의 유효성 검사, 앞뒤 화이트 스페이스 제거, 다른 문자열과 비교
- printf() 로 문자열에 형식 지정하기
- strtolower(), strtoupper(), ucwords() 대소문자 조작
- substr() 문자열 일부 선택
- str_replace() 문자열 부분 교체
- 숫자의 수학적 계산
- 변수 정의 및 값 저장하기
- 변수에 조합 연산자 사용
- 증가 연산자와 감소 연산자
- 문자열 내부에 변수 삽입하기

---
