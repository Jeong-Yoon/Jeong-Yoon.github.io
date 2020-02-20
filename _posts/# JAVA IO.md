# JAVA IO

- File클래스에 대해 살펴봤다.
- 프로그램은 입출력이 기본이다.

- 입력은 어디에서 받을 수 있을까?
    * 키보드
    *  파일
    * 메모리(ex, 배열)
    * 네트워크

- 출력은 어디에 할 수 있을까
    * 화면
    * 파일
    * 메모리
    * 네트워크

- 네트워크도 파일이고 프린트도 파일이다. 어떠한 장치도 파일로 본다.(유닉스 계열에서)

## 특수한 IO(주인공)

- 항상 열려 있음. 닫을 필요가 없음.
    * System.out : 표준 출력 PrintStream – 화면
    * System.in : 표준 입력 InputStream – 키보드
    * System.err : 표준 에러 출력 PrintStream – 화면

- 리다이렉션 기호를 이용해서 출력과 입력 방향을 바꿀 수 있다.


- out.print랑 err.print는 출력을 하면 똑같이 나오지만 유닉스 계열에서 실행을 아래처럼 해보면 따로 저장되는 걸 볼 수 있다.

- java IOExam > out.txt 2> error.txt
    * out.txt파일과 error.txt파일 두 가지가 만들어진다.
> ; 리다이렉션 기호
>   * 표준 출력을 out.txt에 저장하라, 유닉스 계열에서 사용하는 것. 자바 명령어가 아니다.
> * 2> : 표준 에러 출력을 err.txt에 저장하라

>>: 기존 파일에 추가하라.


## 추상 클래스

JAVA IO는 바이트 단위 입출력이 있고, 문자 단위 입출력이 있다.<br>
JAVA 처음 탄생했을 땐 byte단위 입출력만 있었다.

### byte단위 vs char단위
- char단위는 사람이 보는 문자를 입출력 할 때 사용한다.
- 여하튼 byte 단위로도 모두 입출력 할 수 있다.

- InputStream : byte를 읽어 들이기 위한 Stream
- OutputStream : byte를 쓰기 위한 Stream
- Reader : char를 읽어 들이기 위한 Stream
- Writer : char를 쓰기 위한 Stream
    * 위의 추상 클래스는 1개 또는 배열 단위로 읽고 쓰는 메소드를 가지고 있다.


## 주인공과 장식이 있다.

- 위의 4가지 추상 클래스를 상속받고 있는 클래스 중에서, <br>
생성자에 위의 4가지 중 한가지를 받아들이는 생성자가 있는 클래스는 장식.

### 장식
- BufferedInputStream
- BufferedOutputStream
- BufferedReader : readLine() 한줄씩 입력 받는 메소드, 
- BufferedWriter
- DataInputStream : 다양한 데이터 타입을 읽고 쓴다. int, byte, long …
- DataOutputStream
- FilterInputStream
- FilterOutputStream
- FilterReader
- FileWriter
- ObjectInputStream

### 주인공
- ByteArrayInputStream
- ByteArrayOutputStream
- CharArrayReader
- CharArrayWriter
- FileInputStream
- FileOutputStream
- FileReader
- FileWriter
- PipedInputStream

#### 예시
```
만 바이트 짜리 배열이 있는 데 한 줄 씩 읽어 들여라 하면
ByteArrayInputStream, BufferedReader 을 같이 쓰면 된다.

텍스트 파일을 한줄씩 읽어 들여라
FileReader + BufferedReader

키보드로부터 한줄씩 읽어 들여라.
System.in + BufferedReader


~InputStream : byte 단위
~Reader : char 단위

byte -> char 바꾼다.
InputStreamReader
OutputStreamWriter


객체 직렬화와 관련된 Stream
ObjectInputStream
ObjectOutputStream

쓰레드와 같이 사용된다. 스트림을 연결하는 기능을 가지고 있다.
PipedInputStream
PipedOutputStream
PipedReader
PipedWriter

다양한 print(), println()메소드를 제공한다.
PrintStream
PrintWriter


문자열을 읽어 들인다. – 주인공
StringBufferInputStream
StringReader
StringWriter
```

- 주인공은 어디에서 읽어 들일 것인가? 어디에 쓸 것인가? 를 결정하는 클래스
    * 메소드가 간단하다. 어떤 단위로 읽고 쓸 것인가 정도.
- 장식은 어떤 방법으로 읽고 쓸 것인가? 
    * 다양한 메소드를 제공하는 클래스

 



