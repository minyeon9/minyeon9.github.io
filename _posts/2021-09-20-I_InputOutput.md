---
layout: single
title: "입출력(I/O)"
categories: ['Programing', 'Java']
---
   
#### 입출력(I/O)
* Input / Output
* 컴퓨터 내부, 외부 장치와 프로그램 간의 데이터를 주고 받는 것
* 입출력 데이터를 처리할 공통적인 방법으로 스트림 이용
* input / output은 프로그램을 기준으로 생각할 것   
   
***
#### 바이트 기반 스트림
* 바이트 기반 스트림
   
**InputStream(입력)**   
   
* 바이트 기반 입력 스트림의 최상위 추상 클래스
* close() 필수
* 하위 클래스 : xxxInputStream
    * ex) FileInputStream / BufferedInputStream / DataInputStream   
   
**InputStream의 메서드**   
   
|리턴 타입|메서드|설명|
|------|---|---|
|int|read()|입력 스트림으로부터 1바이트를 읽고 읽은 바이트 리턴|
|int|read(byte[] b)|입력 스트림으로부터 읽은 바이트들을 매개 값으로 주어진 바이트 배열 b에 저장하고 실제로 읽은 바이트 수 리턴|
|int|read(byte[] b, int off, int len)|입력 스트림으로부터 len개의 바이트만큼 읽고 매개 값으로 주어진 바이트 배열 b[off]부터 len개까지를 저장, 그리고 실제로 읽은 바이트 수인 len개 리턴, 만약 len개를 모두 읽지 못 하면 실제로 읽은 바이트 수 리턴|
|void|close()|사용한 시스템 자원 반납 후 입력 스트림을 닫음|   
   
   
**OutputStream(출력)**   
   
* 바이트 기반 출력 스트림의 최상위 추상 클래스
* close() 필수
* 하위 클래스 : xxxOutputStream
    * ex) FileOutputStream / BufferedOutputStrema / DataOutputStream / PrintStream
    
**OutputStream의 메서드**   
   
|리턴 타입|메서드|설명|
|------|---|---|
|void|write(int b)|출력 스트림으로 1바이트를 보냄|
|void|write(byte[] b)|출력 스트림에 매개 값으로 주어진 바이트 배열 b의 모든 바이트를 보냄|
|void|write(byte[] b, int off, int len)|출력 스트림에 매개 값으로 주어진 바이트 배열 b[off]부터 len개까지의 바이트를 보냄|
|void|flush()|버퍼에 잔류하는 모든 바이트 출력|
|void|close()|사용한 시스템 자원 반납 후 출력 스트림을 닫음|
   
#### 문자 기반 스트림
* 문자만 주고 받을 수 있음   
   
**Reader(입력)**   
   
* 문자 기반 입력 스트림의 최상위 추상 클래스
* 하위 클래스 : FileReader
    * ex) FileReader / InputStreamReader / BufferedReader
   
**Reader의 메서드**   
   
|리턴 타입|메서드|설명|
|------|---|---|
|int|read()|입력 스트림으로부터 한 개의 문자를 읽고 리턴|
|int|read(char[] c)|입력 스트림으로부터 읽은 문자들을 매개 값으로 주어진 문자 배열 c에 저장하고 실제로 읽은 문자 수 리턴|
|int|read(char[] c, int off, int len)|입력 스트림으로부터 len개의 문자만큼 읽고 매개 값으로 주어진 문자배열 c[off]부터 len개까지 저장, 실제로 읽은 문자 수인 len개 리턴|
|void|close()|사용한 시스템 자원 반납 후 입력 스트림을 닫음|   
   

**Writer(출력)**   
   
* 문자 기반 출력 스트림의 최상위 추상 클래스
* 하위 클래스 : FileWriter
    * ex) FileWriter / InputStreamWriter / BufferedWriter / PrintWriter
   
**Writer의 메서드**   
   
|리턴 타입|메서드|설명|
|------|---|---|
|void|write(int c)|출력 스트림으로 매개 값이 주어진 한 문자를 보냄|
|void|write(char[] c)|출력 스트림에 매개 값으로 주어진 문자 배열 c의 모든 문자를 보냄|
|void|write(char[] c, int off, int len)|출력 스트림에 매개 값으로 주어진 문자 배열 c[off]부터 len개까지의 문자 보냄|
|void|write(String str)|출력 스트림에 매개 값으로 주어진 문자열을 보냄|
|void|write(String str, int off, int len)|츨력 스트림에 매개 값으로 주어진 문자열 off순번부터 len개까지 문자 보냄|
|void|flush()|버퍼에 잔류하는 모든 문자열 출력|
|void|close()|사용한 시스템 자원 반납 후 출력 스트림을 닫음|
   
***
#### File 클래스
* 파일 시스템의 파일을 표현하는 클래스
* 파일 크기, 파일 속성, 파일 이름 등의 정보와 파일 생성 및 삭제 기능 제공
* file 객체 생성   
   
``` java
File file = new File("파일 경로");
File file = new File("C:/data/test.txt");
```   
   
* directory 생성도 가능   
   
**파일 디렉토리 생성 및 삭제 메서드**   
   
|리턴 타입|메서드|설명|
|------|---|---|
|boolean|createNewFile()|새로운 파일 생성|
|boolean|mkdir()|새로운 디렉토리 생성|
|boolean|mkdirs()|경로 상에 없는 모든 디렉토리 생성|
|boolean|delete()|파일 또는 디렉토리 삭제|   
   
**파일/디렉토리 정보 리턴 메소드**   
   
|리턴 타입|메서드|설명|
|------|---|---|
|boolean|canExcute()|실행할 수 있는 파일인지 여부|
|boolean|canRead()|읽을 수 있는 파일인지 여부|
|boolean|canWrite()|수정 및 저장할 수 있는 파일인지 여부|
|String|getName()|파일 이름 리턴|
|String|getParent()|부모 디렉토리 리턴|
|File|getParentFile()|부모 디렉토리를 File객체로 생성 후 리턴|
|String|getPath()|전체 경로 리턴|
|boolean|isDirectory()|디렉토리인지 여부|
|boolean|isFile()|파일인지 여부|
|boolean|isHidden()|숨김 파일인지 여부|
|long|lastModified()|마지막 수정 날짜 및 시간 리턴|
|long|length()|파일 크기 리턴|
|String[]|list()|디렉토리 포함한 파일목록을 String배열로 리턴|
|String[]|list(FilenameFilterfilter)|디렉토리에 포함된 파일 및 서브 디렉토리 목록 중 FilenameFilter에 맞는 것만 String배열로 리턴|
|File[]|listFiles()|디렉토리에 포함된 파일 및 서브 디렉토리 목록 전부File 배열로 리턴|
|File[]|listFile(FilenameFilterfilter)|디렉토리에 포함된 파일 및 서브 디렉토리 목록 중FilenameFilter에 맞는 것만 File배열로 리턴|
   

**FileInputStream**   
   
* 파일을 바이트 단위로 읽을 때 사용
* 모든 종류의 파일 읽기 가능
* InputStream 의 하위 클래스로 InputStream과 사용법 동일
* 객체 생성 시 파일과 직접 연결
    * 파일 미 존재 시 FileNotFoundException 발생 > 예외 처리 필수
   
``` java
FileInputStream fis = new FileInputStream("C:/data/test.txt");
```   
   
**FileOutputStream**   
   
* 바이트 단위로 저장할 때 사용
* 모든 종류의 파일 저장 가능
* OutputStream의 하위 클래스로 OutputStream과 사용법 동일
* 객체 생성 시 파일과 직접 연결
* 파일 미 존재 시 자동으로 생성
* 이미 파일이 존재할 경우 덮어쓰는 단점
   
``` java
FileOutputStream fos = new FileOutputStream("C:/data/test.txt");

// 덮어쓰지 않고 이어 쓰고 싶을 경우 true 작성
FileOutputStream fos = new FileOutputStream("C:/data/test.txt", true);
```
   
**FileReader**   
   
* 텍스트 파일로부터 문자 단위로 읽을 때 사용
* 그림, 오디오, 비디오 파일은 읽기 불가
* Reader의 하위 클래스로 Reader와 사용 방법 동일   
   
**FileWriter**   
   
* 텍스트 파일을 문자 단위로 저장 시 사용
* 그림, 오디오, 비디오 파일 저장 불가
* Writer의 하위 클래스로 Writer와 사용 방법 동일   
   
***
#### 보조스 트림
* 스트림의 기능을 향상시키거나 새로운 기능 추가를 위해 사용
* 단독으로 입출력 처리 불가능   
   
``` java
FileInputStream fis = new FileInputStream("sample.txt"); //기반 스트림 생성
BufferedInputStream bis = new BufferedInputStream(fis); //보조스트림 생성
bis.read(); //보조스트림으로부터 데이터 읽어옴
```   
   
1) 보조 스트림 종류
* 문자 변환(InputStreamReader/OutputStreamWriter)
* 입출력 성능 향상(BufferedInputStream/BufferedOutputStream)
* 기본 데이터 타입 출력(DataInputStream, DataOutputStream)
* 객체 입출력(ObjectInputStream/ObjectOutputStream) 등
   
**문자 변환 보조 스트림**   
   
* InputStreamReader, OutputStreamWriter
* 소스 스트림이 바이트 기반 스트림이지만 데이터가 문자일 경우 사용
* Reader와 Writer는 문자 단위로 입출력을 하기 때문에 데이터가 문자인 경우 바이트 기반 스트림보다 편리하게 사용 가능
   

**성능 향상 보조 스트림**   
   
* BufferedInputStream/Reader, BufferedOutputStream/Writer
* 느린 속도로 인해 입출력 성능에 영향을 미치는 입출력 소스를 이용하는 경우 사용
* 입출력 소스와 직접 작업하지 않고 버퍼에 데이터를 모아 한꺼번에 작업을 하여 실행 성능 향상(입출력 횟수 줄임)
   
   
**기본 타입 입출력 보조 스트림**   
   
* 기본 자료형 별 데이터 읽고 쓰기가 가능하도록 기능 제공
* 입력된 자료형의 순서와 출력될 자료형의 순서 일치 필수   
   

**객체 입출력 보조 스트림**   
   
* 객체를 파일 또는 네트워크로 입출력 할 수 있는 기능 제공
* 객체는 문자가 아니므로 바이트 기반 스트림으로 데이터를 변경해주는 직렬화 필수

***
