# CHAPTER 9. 파일 다루기

- 특정 파일에 대한 읽기 쓰기 권한 제어
- 파일에서 데이터를 읽어 들이고 기록하는 기술
- 파일 처리 작업 중 발생할 수 있는 오류를 처리하는 기법

## 9.1 파일 접근 권한

- 파일의 읽기/쓰기 권한은 운영체제가 PHP 엔진에 부여함  
- PHP 인터프리터는 웹 서버 내뷰에서 실행되며 '웹 서버를 실행하는 계정'의 권한을 부여받음  
- 따라서 특정 파일이나 디렉터리를 열람할 수 있는 권한이 웹서버에 있다면,  
    PHP 엔진(또한 PHP 프로그램)은 그 파일이나 디렉터리를 열람할 수 있다.



## 9.2 전체 파일 읽고 쓰기

### 9.2.1 파일 읽기

- file_get_contents()
파일명을 전달받고 해당 파일의 모든 내용을 문자열로 반환한다.
```js
// page-contents.html 파일 불러오기
$contents = file_get_contents('contents.txt');
```

### 9.2.2 파일 일부분 읽고 쓰기

- file_put_contents()  
파일명, 저장할 내용을 전달받고 해당 파일의 내용을 전달 받은 문자열로 변경
```js
$contents = file_get_contents('contents.txt');
$contents .= "파일 하단에 내용을 추가합니다.";
// page-template.html 파일에 $pageContents 의 값을 기록
file_put_contents('page-contents.html', $contents);
```

## 9.3 파일 일부분 읽고 쓰기
- **file( string $filename )**  
    파일의 각 줄에 해당하는 문자열(개행문자 포함)을 배열로 반환한다.  
    _file('user.txt')_  
- **fopen( string $filename , string $filemode )**  
    파일에 접속하고, 이후 프로그램에서 사용할 수 있는 파일 접근 변수 반환  
    (8장의 new PDO() 가 반환하는 DB 접속 변수와 개념적으로 유사함)  
    \* 접근할 파일명  
     \- 경로구분자로 슬래시(/) 이용  
     \- 윈도우의 경우 역슬래시를 슬래시로 대체  
    \* 파일모드  
     \- 해당 파일에 어떤 작업을 허용할지 결정(읽기, 쓰기 권한)  
     \- PHP 엔진이 파일을 읽기 시작할 위치, 내용 초기화 여부, 파일이 없을 경우 대응법 등  
    _$file = fopen('c:/project/user.txt', 'rb')_  
    _$file = fopen('userlog.txt', 'ab')_  

- **fgets( $file )**  
    파일 내용을 한 줄씩 읽고 문자열로 반환  
    PHP 엔진은 파일을 읽어들일때, 파일의 맨 앞에서부터 현재 읽고 있는 위치를 표시해 둔다.  
    fget()를 처음 호출하면 파일의 첫번째 줄을 읽고, 위치 표시를 다음 줄의 처음 부분으로 이동시킴  
    _fgets($file)_
- **fwrite( $file, string $string )**  
    파일에 내용을 기록  
    _fwrite($file, "해당 파일에 기록할 내용")_
- **feof( $file )**  
    위치 표시가 파일의 끝을 지나면 true를 반환(end of file)  
    _feof($file)_
- **fclose()**  
    파일 접속을 닫음  
    _fclose($file)_



|모드|허용 작업|시작 위치|내용 초기화|파일이 없을 때|
|---|---|---|---|---|
|rb|읽기|파일의 처음|아니오|경고 발생 후 false 반환|
|rb+|읽기, 쓰기|파일의 처음|아니오|경고 발생 후 false 반환|
|wb|쓰기|파일의 처음|예|새로 생성|
|wb+|읽기, 쓰기|파일의 처음|예|새로 생성|
|ab|쓰기|파일의 마지막|아니오|새로 생성|
|ab+|읽기, 쓰기|파일의 마지막|아니오|새로 생성|
|xb|쓰기|파일의 처음|예|새로 생성 시도, <br>파일이 존재하면 경고 발생 후 false 반환|
|xb+|읽기, 쓰기|파일의 처음|예|새로 생성 시도, <br>파일이 존재하면 경고 발생 후 false 반환|
|cb|쓰기|파일의 처음|아니오|새로 생성|
|cb+|읽기, 쓰기|파일의 처음|아니오|새로 생성|




event.txt 파일 내용
```
이벤트명|시작일|종료일|참여자수
스티커 이벤트|2017.04.11|2017.04.15|1000명
이미지합성|2017.05.15|2017.05.31|제한없음
```
event.txt 파일의 각 줄 내용 일부 출력  
```js
foreach(file('event.txt') as $line){
    $line = trim($line);            // 문자열 끝의 개행문자를 제거한다.
    $info = explode("|", $line);    // | 구분자로 문자열을 분리

    	print $info[0].' : '.$info[3]."<br>";
}
/*
이벤트명 : 참여자수
스티커 이벤트 : 1000명
이미지합성 : 제한없음
*/
```


전체 파일을 읽고 모든 줄을 배열로 만들기 때문에  
용량이 큰 파일의 경우 내용을 한줄씩 읽어들인다 &rarr; fgets($file)
```js
$file = fopen('event.txt', 'rb');       // event.txt 를 읽기전용으로 열기
while ((! feof($file)) && ($line = fgets($file))){
	$line = trim($line);
	$info = explode("|", $line);

	print $info[0].' : '.$info[1]."<br>";
}
fclose($file);
/*
이벤트명 : 시작일
스티커 이벤트 : 2017.04.11
이미지합성 : 2017.05.01
*/
```



## 9.4 CSV 파일 다루기

- **CSV 파일**  
    여러 프로그램 사이에서 표 데이터를 효과적으로 공유할 수 있음

```js
try{
    $db = new PDO('sqlite:/tmp/event.db');
} catch(Exception $e){
    print "DB에 접속할 수 없습니다 : " . $e->getMessage();
    exit();
}

// event.txt 파일을 쓰기 모드로 열기
$file = fopen('category.txt', 'wb');

$stmt = $db->prepare('INSERT INTO event (category1, category2, title) VALUES (?, ?, ?)');
//query("SELECT title, start_date, end_date, total_count FROM event");
while(! feof($file) && ($info = fgetcsv($file))){
    // 각 줄을 파일에 쓰고 마지막에 개행문자 추가
    $stmt -> execute($info);
    print "$info[0] 추가되었습니다.\n"
    fwrite($file, "$row[0]의 총 참여자 수는 $row[3]\n");
}
if(! fclose($file)){
    print "event.txt 파일을 닫을 수 없습니다 : $php_errormsg";
}

```

- **fgetcsv()**  
    csv 파일 내용의 한 줄을 읽고 각 필드값을 담은 배열을 반환   

```js
// event.txt 파일을 읽기 모드로 열기
$file = fopen('board.csv', 'rb');

$stmt = $db->prepare('INSERT INTO BOARD (board_type, title, content, reg_id) VALUES (?, ?, ?, ?)');
//query("SELECT title, start_date, end_date, total_count FROM event");
while(! feof($file) && ($info = fgetcsv($file) ) ){
    // 각 줄을 파일에 쓰고 마지막에 개행문자 추가
    $stmt -> execute($info);
    print "$info[1] 추가되었습니다.\n";
    //fwrite($file, "$row[0]의 총 참여자 수는 $row[3]\n");
}
if(! fclose($file)){
    print "board.csv 파일을 닫을 수 없습니다 : $php_errormsg";
}
```

## 9.5 파일 권한 확인
- **file_exists()**  
    파일이 존재하는지 확인
    file_exists('filename') &rarr; true/false
- **is_readable()**  
    읽기 권한 테스트
    is_readable('filename') &rarr; true/false
- **is_writeable()**  
    쓰기 권한 테스트
    is_writeable('filename') &rarr; true/false

## 9.6 오류 검사
안전한 파일 처리 코드를 작성하기 위해 파일 관련 함수의 반환값을 확인  
파일 함수는 문제가 발생하면 경고 메시지를 생성하고 false 반환  
track_errors 설정이 활성화되어있으면 오류 메시지 텍스트가 전역변수 $php_errormsg 에 저장된다.  

**fopen(), fclose() 오류 확인하기**
```js
try{
    $db = new PDO('sqlite:/tmp/event.db');
} catch(Exception $e){
    print "DB에 접속할 수 없습니다 : " . $e.getMessage();
    exit();
}

// event.txt 파일을 쓰기 모드로 열기
$file = fopen('sample.txt', 'wb');
if(! $file){
    print "event.txt 파일을 열 수 없습니다 : $php_errormsg";
    // event.txt 파일을 열 수 없습니다 : failed to open stream: Permission denied
}else{
    $q = $db->query("SELECT title, start_date, end_date, total_count FROM event");
    while($row = $q->fetch()){
        // 각 줄을 파일에 쓰고 마지막에 개행문자 추가
        fwrite($file, "$row[0]의 총 참여자 수는 $row[3]\n");
    }
    if(! fclose($file)){
        print "event.txt 파일을 닫을 수 없습니다 : $php_errormsg";
    }
}
```
 운영체제는 가끔 fwrite() 함수를 호출할 때 데이터를 파일에 바로 쓰지 않고 버퍼에 저장하는데 기록할 데이터에 비해 디스크 여유공간이 부족하면 fclose() 호출시 오류가 발생

fgets(), fwrite(), fgetcsv(), file_get_contents(), file_put_contents() 등의 함수는 반환값을 이용해 별도의 처리 과정을 거쳐야 함 정확한 확인을 위해 동일비교연산자인 삼중등호(===) 사용  

**file_get_contents() 오류 확인**
```js
$page = file_get_contents('event.txt');
// 삼중등호를 이용한 조건 표현식
if($page === false){
    print "파일을 불러올 수 없습니다 : $php_errormsg";
}else{
    // 처리부분
}
```

**fopen(), fgets(), fclose() 오류 확인**
```js
$file = fopen('userinfo.txt', 'rb');
// 삼중등호를 이용한 조건 표현식
if(! $file){
    print "파일을 열 수 없습니다 : $php_errormsg";
}else{
    while(! feof($file)){
        $line = fgets($file);
        if($line !== false){
            $line = trim($line);
            $info = explode('|', $line);
            print "<tr><td>$info[1]</td><td>$info[2]</td></tr>";
        }
    }
    if(! fclose($file)){
        print "userinfo.txt 파일을 닫을 수 없습니다 : $php_errormsg";
    }
}
```
## 9.7 외부에서 입력받은 파일명 처리
- 폼 또는 URL로 전달받은 데이터를 정제 없이 이용시 크로스 사이트 스크립팅(XSS;Cross Site Scripting) 및 SQL 주입 공격 위험
- 파일명 또는 경로에 쓰이는 문자열 처리 필요  
ex) 경로 구분자(/), 상위 디렉터리 표시자(..)

**파일명에 들어갈 폼 매개변수를 안전하게 조치하기(str_replace)**
```js
// 파일명에서 경로 구분자(/) 제거
$user = str_replace('/', '', $_POST['user']);
// 파일명에서 상위 디렉터리 표시자(..) 제거
$user = str_replace('..', '', $user);

if(is_readable("/usr/local/data/$user")){
    print "파일명 : ".htmlentities($user)."<br>";
    print file_get_contents("/usr/local/data/$user");
}else{
    print "파일을 찾을 수 없습니다.($user)";
}
```

**realpath()로 파일명 처리**
```js
$filename = realpath("/usr/local/data/$_POST[user]");
//$filename 이 해당 폴더에 존재하는지 확인
//print "realpath : $filename ".dirname(__FILE__)."<br>";
if(('/usr/local/data/' == substr($filename, 0, 16)) && is_readable($filename)){
    print "파일명 : $_POST[user]<br>";
    print "실제파일경로 : $filename<br>";
    print file_get_contents($filename);
}else{
    print "$_POST[user] 파일이 존재하지 않습니다.<br>$filename";
}
```


## 9.8 마치며
- PHP 엔진의 파일 접근 권한 기준
- file_get_contents()로 파일 전체 읽기
- file_put_contents()로 파일 전체 쓰기
- file()로 파일의 모든 줄을 배열로 얻기
- fopen()과 fclose()로 파일 열고 닫기
- fgets()로 파일을 한 줄 읽기
- feof()와 while() 루프로 파일을 한 줄씩 읽기
- 모든 운영체제에서 작동하도록 파일명에 슬래시 사용하기
- fopen() 에서 사용하는 다양한 모드
- fwrite()로 파일에 데이터 쓰기
- fgetcsv()로 CSV 파일을 한 줄 읽기
- fputcsv()로 CSV 파일을 한 줄 쓰기
- php://output 스트림을 이용해 출력하기
- file_exists()를 이용해 파일의 존재 여부 확인하기
- is_readable()과 is_writeable()을 이용해 파일 사용 권한 확인하기
