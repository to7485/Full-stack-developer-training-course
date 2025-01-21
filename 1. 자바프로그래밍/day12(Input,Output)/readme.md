# 파일 입출력
## 자바 입출력과 스트림
- 프로그램은 데이터를 외부에서 입력받아 처리하고 출력하는 구조로 되어 있습니다.
- 프로그램으로 들어오는 모든 값을 Input이라고 한다.
- 프로그램을 나가는 모든 값을 Output이라고 한다.
- 자바에서는 입출력을 처리하기 위해 별도의  I/O패키지를 제공한다.
- 데이터는 자바에서 처리할 수 있는 모든것을 의미한다.
- 디스크상에 존재하는 데이터일 수도 있고, 키보드나 마우스와 같은 외부입력 장치에서 입력되는 데이터일 수도 있고,
- 인터넷을 통해 전송되는 데이터일 수도 있다.
- 자바가 디스크에 접근에 데이터를 주고받는 작업을 도와주는 통로를 '스트림(stream)'이라고 한다.

![image](https://user-images.githubusercontent.com/54658614/221475515-1bbfdce7-6880-413f-8023-3d5fbd43f2b7.png)

## File클래스
- 파일 또는 폴더에 대한 정보를 제공하는 클래스
- 경로명, 파일 크기, 타입, 날짜 등의 속성 정보를 제공한다.
- 파일 생성, 삭제, 이름 변경 등 파일 관리 작업을 지원하기 위한 메서드로 구성되어 있다.

### Ex1_File 클래스 정의
```java
test.txt 문서를 만들고 안녕하세요abc 라고 적은 뒤에 d:/에 가져다 놓은 뒤에 코드 작성

public class Ex1_File {
public static void main(String[] args) {

우리가 늘 작업하던 경로로 들어와서 메모장을 만든다.web_14.lhj
test.txt 
보기탭 누르고 파일 확장명 체크 되어있는지 확인
안녕하세요 작성 후 다른이름으로 저장

문자열이 나열된 형태가 타입이 utf-8 아스키코드에 존재하지 않는 언어를
깨지지 않게 표시하기 위한 언어형태
ANSI로 저장하기 자바에서 테스트 하는 동안에만 ANSI로 저장할꺼임

// 파일 객체를 생성할 경로 
String path = "d:/web_14_java/test.txt";  
        
// 준비된 경로로 File객체 생성   
File f = new File(path);
//File 클래스가 생성되면서 path경로까지 스트림을 생성

통로를 만들어 준다고 생각하면 된다. 앞으로 내가 만든 파일 이라는 클래스는 path까지 다이렉트로 접근하는 터널같은 것. 중간에 경로가 잘못 되지 않았는지까지도 판별해준다.
        
//f.isFile() : 파일클래스가 접근한 최종 목적지가 파일형식일 경우 true	if(f.isFile()){// 생성된 객체가 파일일 경우 !f.isFile() 
    System.out.println(f.length() + "byte"); 한글은 2byte, 영문 특수문자 1byte 
폴더의 용량도 가져올 수 있다. 파일이든 폴더든 나의 최종 목적지에 해당하는 용량을 가져올 수 있다.
  }
}

```

### Ex2_File 클래스 정의

```java
public class Ex2_File {	
  public static void main(String[] args) {
  // 파일객체로 쓰인 경로
  String path = "D:/web14_lhj/";
  //강의에 사용중인 폴더 경로 지정 \\ 쓰려면 두 개 써줘야 함
 

  //파일클래스가 할 수 있는 두번째 기능 : 폴더를 찾았을 때 내 폴더의 하위 요소들의 이름을 문자열 배열로 반환한다.

  File f = new File(path);
  //파일클래스가 접근하고자 하는 최종 목저지는 폴더까지... 폴더까지 접근해야 하위 목록들의 이름을 가져올 수 있음 파일은 하위 목록이 없기 때문


  if(!f.isFile()){ //파일이 아닐경우,!f.isFile()), f.isDirectory() 애초에 폴더인지 판별하는 메서드도 가지고 잇다.
  // 디렉토리 안에있는 하위 요소들의 이름을 모두 가져온다.
  String[] names = f.list(); 반환형 String[] //f경로의 하위 요소들을 names배열에 저장

  list()메서드는 내가 접근한 경로에 하위 목록을 배열형태로 정렬을 해서 이름을 알파벳 순서대로 정렬까지 한다. 

  직접 세보지 않고도 파일 클래스를 통해서 하위 요소들이 총 몇 개인지를 알아서 list라고 하는 메서드가 구해준다.
  비어있는공간이 없도록 딱 맞는 공간에 맞게 크기를 제공한다.

  경로를 입력 받을수도 있어서 배열의 크기를 미리 만들어 놓을수가 없다.

  파일 클래스에는 폴더인지 파악하는 기능, 하위 요소들의 이름을 꺼내 오는 기능도 있다.

//개선된 roop문
for(String s : names) {
    System.out.println(s);	
    }	
  }
}
```

### Ex3_File 클래스 정의

```java
public class Ex3_File {	
	public static void main(String[] args) {	

String path = "D:/web14_lhj/aaa/bbb";//만들어질 폴더

File f1 = new File(path);
aaa라고 하는 폴더가 물리적으로 존재하지 않는다
내가 최종 목적지 까지 가는 길에 혹시라도 길이 존재하지 않는 경로가 포함되어있지 않은지 판단할 수 있어요.

//exists() : 파일 클래스가 path경로로 찾아가는 중
//정상적으로 폴더나 파일이 존재한다면 true를 반환
if(!f1.exists()){ //f.exists() == false
System.out.println("폴더생성");
f1.mkdirs();//폴더생성

코드를 통해서 목적지를 자동으로 만들어준거다.
실제로 되게 많은 프로그램들이 이런 기능들을 가진 클래스를 거진 가지고 있다.

파일클래스는 특정 문서를 만드는 기능은 없다 클래스 파일은 폴더만드는거 까지만 가능하다.

    	}
   }
}
```
## 입출력 스트림의 종류
- 자바의 기본적인 데이터 입출력은 java.io 패키지에서 제공한다.
- java.io패키지에서는 파일 시스템의 정보를 얻기 위한 File클래스와 데이터 입출력을 위한 다양한 스트림 클래스를 제공한다.
- 스트림의 종류를 크게 분류하면 전달 방식에 따라 바이트(byte)기반 스트림과 문자(char)기반 스트림으로 구분한다.
- 바이트 기반의 스트림은 데이터를 컴퓨터의 기본 단위인 byte단위로 나누어 읽거나 쓰고,
- 문자 기반 스트림은 텍스트 기반 문서를 다루기 위해 사용하는 스트림이다.

![image](https://github.com/to7485/Java1900/assets/54658614/ef011e69-53f8-4724-8984-6540d80bb661)

## 바이트(byte)기반 스트림
- 컴퓨터의 모든 데이터는 바이트(byte)단위로 이루어져 있다.
- 따라서 바이트 기반 스트림의 경우 모든 타입의 데이터를 읽고 쓰는 것이 가능하다.
- 바이트 기반의 스트림은 바이트 입력 스트림과 바이트 출력 스트림이 있다.

## InputStream
- 바이트 기반의 입력 스트림은 최상위 클래스로 InputStream객체가 제공된다.
- 해당 객체를 상속해 다양한 입력 스트림들이 존재한다.

![image](https://github.com/to7485/Java1900/assets/54658614/65ef0bee-cb84-493e-ad38-33ae480aa8ab)

- 모두 InputStream을 상속하여 다양한 입력 스트림을 구현하고 있다.
- 각자의 개발 목적에 맞게 성택하여 사용할 수 있다.
- 예를 들어 파일을 읽어서 사용하고 싶다면 FileInputStream객체를 선언해 사용하면 된다.

## InputStream의 주요 메서드
|메서드|설명|
|------|-----|
|int read()|문자를 1byte씩 읽고 반환<br>더 이상 읽을 문자가 없으면 -1을 반환|
|int read(byte[]b)|매개변수로 주어진 배열에 읽은 문자를 저장하고 실제로 읽은 수만큼 반환<br>더 이상 읽을 문자가 없으면 -1을 반환|
|int read(byte[],int offset,int len)|매개변수로 주어진 배열에 정해진 범위만큼 읽어서 저장<br>시작 위치(offset), 길이(len)|
|int available() | 스트림으로부터 읽어올 수 있는 데이터의 크기를 변환|
|close() | 스트림 사용을 종료하고 자원을 반환|

## FileInputStream
- FileInputStream은 파일에서 바이트 단위로 자료를 읽어들일 때 사용하는 스트림이다.
- 이미지,동영상,텍스트 등 모든 타입의 파일을 읽어올 수 있다.

### Ex1_FileInputStream 클래스
```java
public class Ex1_FileInput {
	public static void main(String[] args) {

	Stream에 대한 특징


	String path = "D:/web14_lhj/test.txt";
	//위 예제에서 만든 test.txt문서

	File f = new File(path);
	파일 클래스를 만들어서 경로에 오타가 났다거나 없는 경로가 있지 않은지 탐사를 보내요~

	if(f.exists()){ //파일이 실제 존재할 때만 수행!
		try{
			// 파일클래스가 가진 경로로 접근하기 위한 입력 스트림 생성	
			FileInputStream fis = new FileInputStream(f);
			밖에 있는걸 읽어올거야~ test.txt까지 읽어오는 스트림을 만들거야
			try-catch FileNotFoundException e 너가 위에서 답사를 했지만 혹시라도 내가 만들어질 때 지정해놓은 파일이 없어질 가능성이 있다.
			예측은 가능하지만 잡을수는 없는 오류이다. 그래서 try-catch로 강제로 묶어야 한다.

			// 스트림은 더 이상 읽을 것이 없다면 -1을 반환하게 되어 있다.
			// 즉 파일의 모든 내용을 읽어오기 위해 반복문을 수행하고
			// 그 반복은 파일의 끝(EOF)인 -1을 만날 때까지 반복하면 된다.

			int code = 0;

			fis는 txt까지 접근하는 작업 read라는 메서드가 안에있는 글자를 읽어오는 작업을 한다.
			read()메서드는 한번에 한번에 한글자만 읽을 수 있음 안타까운점은 read라는 메서드가 텍스트를 가지고 올 때 1byte씩 밖에 읽어오지 못한다.
			fis는 한글데이터를 읽는게 불가능 하다. 지금 당장은 기본적으로 read를 통해서 읽어올 때는 1byte로 밖에 읽어올 수 없기 때문에 2byte로 이루어진 한글은
			불가능하다.	

			//read()메서드는 한번에 1byte씩 읽어오다가
			//더이상 읽어올 단어가 업다면 문장의 끝(End Of File)인 –1을 가져온다.
			아스키코드, 유니코드에서도 –1를 갖고 있는게 없기 때문에 –1로 정함
			while((code = fis.read()) != -1) {

			//이것을 int 자료형에 담아 char로 형변환하여 출력하면
			//아스키 코드값으로 변경되어 출력되기 때문.
   				System.out.print((char)code); 
   			}

			//스트림은 사용이 완료된 이후 close를 통해 닫아주는 것이 좋다.
			//그래야 다음 작업을 하는데 문제가 생기지 않는다. 
			//close를 작성하지 않았을 때 아직도 할 작업이 남았으니까 화면에 띄우거나 파일을 만들면 안되겠구나 착각하는 경우가 있기 때문이다.
		 	fis.close();
			read메서드 사용하면 IOException 만들어짐 그래서 그냥 Exception 만들고 한번에 처리
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
```

### Ex2_FileInput클래스
```java
public class FileInput {
public static void main(String[] args){

	String path = "D:/web14_lhj/test.txt";

	File f = new File(path);
	//넉넉하게 100. 배열은 int범위까지만 만들 수 있다.
	byte [] read = new byte[(int)f.length()];

	배열의 크기를 딱 맞춰서 메모리 낭비를 하지 않는게 좋지만 키보드에서 그때그때 다른 파일을 받는다면 용량을 알 수 없다.
	근데 length()가 long타입이라서 (int)로 형변환을 해야한다.
	
	if(f1.exists()){ //파일이 실제 존재할 때만 수행!
	   try{
		FileInputStream fis = new FileInputStream(f);

		//read()는 한 바이트씩 읽어들이지만,
		//read(byte[]b)는 배열 btye[]b를 이용해서 한꺼번에 바이트 개수를 읽어온다.
		//그래서 반복문을 쓰지 않아도 된다.
		fis.read(read);

 		//fis가 읽어온걸 read 배열에 넣어주는데 방 두 개를 점유하면서 한글이 저장된다.
 		//현재 byte[]인 read에는 test.txt.에서 읽어온 데이터들이 저장되어 있다.
		//이를 문자열 형태로 재조합하여 출력할 수 있다.
		String res = new String(read); 
		스트링 클래스에 생성자가 오버로딩이 굉장히 많이 되어있다. 그중에 바이트 배열을 넣어주면 문자열로 바꿔주는 오버로딩이 있다.

		바이트 형태로 가져오는 바람에 한글이 다 깨진다면 배열을 준비해서 그 배열에 담긴 값을 문자열로 바꿔보면 어때? 라고 하는 차선택이 있다는 겁니다.
		System.out.println(res);

		//스트림 사용을 완료한 뒤에는 반드시 닫아주자!!
		fis.close();
 	   } catch(Exception e) {
		e.printStactTrace();
	   }
   	}
   }
```
### Ex3_FileInput클래스 정의 – Scanner의 원리
```java
public class FileInput {
	public static void main(String[] args) {

	byte [] keyboard = new byte[100];

	try {
	System.out.print("값: ");
	//키보드에 값을 입력받기 위한 표준입력장치 스트림
	System.in.read(keboard);
	 
	String s = new String(keboard).trim();
	System.out.println(s)

	Scanner sc = new Scanner(System.in);
	//sc.close();

	System.in이 스테틱이라서 메모리에 한번만 올라가고 close로 닫게 되면 다른 클래스에서도 닫아진다.
	} catch ( IOException e) {

	}
```

### 자바 강의 3주차(1) 문제(회문수) 풀기
- 특정 경로에 file.txt문서를 만들고 내용으로 아무 문장이나 입력해둔다
- file.txt의 내용을 FileInputStream으로 읽어온 뒤, 이 값이 회문수인지 아닌지를 판단하시오.

### ex1_work 클래스 생성
```java
public class Ex1_work{
public static void main(String[] args) {
	String path = "d:/file.txt";
	
	File f = new File(path);
	byte[] read = new byte[(int)f.length()]; //txt파일의 크기만큼의 배열 생성

	try{
	   if(f.exists()) {
	   	FileInputStream fis = new FileInputStream(f);
		fis.read(read);//fis가 읽어온 내용을 byte배열에 저장

		//read배열을 String타입으로 변경
		String ori = new String(read);
		String rev = "";
		//String rev = null;  null이라고 하는 코드가 초기화 하는데 사용이 되면 		
		//heap 영역에 메모리 할당 자체가 안되어 있는다는 뜻. String 클래스는 			
		//집을 만들었는데 일단 비워놓는다는 의미로 ""로 초기화를 많이한다.
		
		rev += 1; --> rev = rev + 1; --> rev ="1";
		rev = null; --> rev += 1; --> rev = null + 1; --> rev = "null1"

		//원본문자열인 ori를 뒤집어서 rev객체에 저장
		for(int I = ori.length()-1; I>=0; I--) {
			rev+=ori.charAt(i);
		}//for
		if(ori.equals(rev)) {
			System.out.println(ori + "는 회문수입니다");
		} else {
			System.out.println(ori + "는 회문수가 아닙니다"):
		}
	   fis.close()
	  }//if
	} catch( Exception e) {

	}//try - catch
    }//main
}
```
## OutputStream
- 바이트 기반의 출력 스트림은 최상위 클래스로 OuputStream 객체가 제공된다.
- 해당 객체를 상속해 다양한 출력 스트림들이 존재한다.

![image](https://github.com/to7485/Java1900/assets/54658614/95317635-e5ba-4f01-a94b-1dd6dc61ce1e)

## OutputStream의 주요 메서드
|메서드|설명|
|------|-----|
|int write(int b)|1byte 출력|
|int write(byte[]b)|매개변수로 주어진 배열의 모든 바이트 출력|
|int write(byte[],int offset,int len)|매개변수로 주어진 배열에 정해진 범위만큼 읽어서 출력<br>시작 위치(offset), 길이(len)|
|int flush() | 출력 버퍼에 장류하는 모든 내용 출력|
|close() | 스트림 사용을 종료하고 자원을 반환|

## FileOutputStream
- 파일을 쓸 때 기존 파일명이 존재하는 경우가 있다.
- 이때 해당 파일의 내용을 유지한 채 이어 쓰거나 기존의 내용을 무시하고 새롭게 파일을 생성할 수 있다.
```java
new FileOutputStream(경로/파일명, 이어쓰기 옵션);
```
- 이어쓰기 옵션이 true이면 기존 파일에 이어서 내용을 추가하고, false면 기존 내용을 무시하고 새로 쓰게 된다.
- 기본 옵션은 false로 되어있다.

### Ex1_FileOutput – 출력하기 위한 스트림

```java
public class Ex2_FileOutput{
	public static void main(String[] args) {

	try{
	//내가 기록하려고 할 때 드라이브가 뻑이난다던지 폴더가 사라질수 있기 때문에 try-catch에 넣는다.
	FileOutputStream fos = new FileOutputStream("d:/fileOut.txt");

	fos.write('f');
	fos.write('i');
	fos.write('l');
	fos.write('e');
	이렇게 하면 코드가 지나치게 길어지고 한글을 쓸 수가 없다.

	String msg = "fileOutput 예제입니다.\n";
	String msg2 = "여러줄도 가능";

	//파일에 작성을 하려고 하는데 없으니 파일을 같이 만들어준다.
	//이상태로 실행을 해보면 놀랍게도 우리가 지정한 경로에 fileOut 이라고 하는 파일이 만들어져있고 write한 내용도 기록되있다.
	//세이브파일을 만든다거나 저장하는 문서를 만드는 경우에 요렇게 outputStream이 사용이 된다.
	//확장자도 마음대로 지정할 수 있다.

	fos.write(msg.getBytes());//문자열 msg를 byte[]로 변경하는 메서드
	fos.write(msg2.getBytes());

	fos.close();
	} catch( Exception e) {
	
	}
    }//main
}

```

### read()와 write()를 이용한 이미지 복사
- Ex1_CopyTest 클래스
```java
package test;

import java.io.FileInputStream;
import java.io.FileOutputStream;

public class Ex19_05 {
	public static void main(String[] args) {
		FileInputStream in = null;
		FileOutputStream out = null;
		
		try {
			in = new FileInputStream("C:\\Users\\ITSC\\Desktop\\java/wall.jpg");
			out = new FileOutputStream("C:\\Users\\ITSC\\Desktop\\java/wall_copy.jpg");
			
			//현재 시간을 m/s단위로 나타냄
			long start = System.currentTimeMillis();
			System.out.println("이미지 읽기 시작");
			int read = 0;
			while((read = in.read()) != -1) {
				out.write(read);
			}
			System.out.println("이미지 읽기 종료");
			long end = System.currentTimeMillis();
			long time = (end - start)/1000;
			System.out.println(time+"초");
		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if(out != null) {
					out.close();
				}
				if(in != null) {
					in.close();
				}
			}catch (Exception e) {
				// TODO: handle exception
			}
		}
	}
}
```
- 복사를 하는데 약 17초의 시간이 걸렸다.
- 배열을 이용해서 복사를 할 때는 얼마나 걸리는지 확인해보자

### Ex2_CopyTest2
```java
package test;

import java.io.FileInputStream;
import java.io.FileOutputStream;

public class Ex19_05 {
	public static void main(String[] args) {
		FileInputStream in = null;
		FileOutputStream out = null;
		
		try {
			in = new FileInputStream("C:\\Users\\ITSC\\Desktop\\java/wall.jpg");
			out = new FileOutputStream("C:\\Users\\ITSC\\Desktop\\java/wall_copy.jpg");
			byte[] buffer= new byte[512];
			
			//현재 시간을 m/s단위로 나타냄
			long start = System.currentTimeMillis();
			System.out.println("이미지 읽기 시작");
			
			int read = 0;
			while((read = in.read(buffer)) != -1) {
				out.write(buffer,0,read);
			}
			
			System.out.println("이미지 읽기 종료");
			long end = System.currentTimeMillis();
			double time = (double)(end - start)/1000;
			System.out.println(time+"초");
		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if(out != null) {
					out.close();
				}
				if(in != null) {
					in.close();
				}
			}catch (Exception e) {
				// TODO: handle exception
			}
		}
	}
}
```
- 바이트 배열을 이용하여 이미지를 복사했을 때 처음에 비해 속도가 눈에 띄게 향샹된 것을 확인할 수 있다.

## 문자 기반 스트림
- 자바에서는 기본 자료형은 char형을 통해 문자를 저장할 수 있다.
- 1byte 단위로 처리하는 바이트 기반 스트림은 모든 파일을 다룰 수 있으나 문자를 처리하는 char형의 크기는 2byte로 별도의 처리를 하지 않으면 정상적으로 읽지 못하는 경우가 있다.
- 이때, 문자 기반의 스트림을 사용하면 간단하게 문자를 처리할 수 있다.

## Reader : 문자 입력 스트림
- 문자 기반 입력 스트림은 최상위 클래스인 Reader를 상속해 다양한 클래스를 제공한다.

![image](https://github.com/to7485/Java1900/assets/54658614/18e86518-c340-4111-85f1-3161e1271319)

## 문자기반 스트림에서 제공하는 메서드
|메서드|설명|
|-----|-----|
|int read()|1개의 문자를 읽고 반환<br>더 이상 읽을 문자가 없으면 -1를 반환|
|int read(char[] buf)|매개변수로 주어진 배열에 읽은 문자를 저장하고 읽은 수만큼 반환<br>더 이상 읽을 문자가 없으면 -1를 반환|
|int read(char[] cbuf,int offset,int len)|매개변수로 주어진 배열에 정해진 범위만큼 읽어서 저장<br>시작위치(offset),길이(len)|
|close()|스트림 사용을 종료하고 자원을 반환|

## FileReader
- FileReader는 앞에서 학습한 FileInputStream의 기능들과 메서드의 이름이 같다.
- 기능의 사용법도 크게 다르지 않다.

### Ex1_FileReader 클래스 생성 – 데이터를 읽어오는 작업
```java
Ex1_FileReader{
	public static void main(String[]args) {
	
	   //char기반의 스트림은 Reader, Writer의 자식 클래스들을 사용
	   //기본적으로 2byte를 지원하기 때문에 2byte언어로 구성된 파일도 쉽게
	   // 입출력이 가능
	try{
	   FileReader fr = new FileReader("D:/web14_lhj/test.txt");
	   int code = 0;
	   
	   while((code=fr.read() != -1) {
		System.out.print((char)code);
		System.out.print(code + " ");
	1byte는 아스키 코드로 읽고 2byte는 유니코드로 알아서 읽어서 문자가 깨지거나 하는일이 없다.
	이게 더 좋은거 같은데 음악 파일같은거 전송할 때는 2바이트씩 전송하는게 좋지 않을 수 있다.
	100피스짜리 퍼즐을 옆으로 똑같이 옮긴다고 생각하면 한주먹씩 주는거보다 하나씩 주는게 상식적으로 훨씬 빠를것이다. 
	   }
		fr.close();
	} catch(Exception e) {
	
	}
     }//main
}
```


#### Ex2_FileReader클래스
```java
public class Ex2_FileReader{
	public static void main(String[] args) {

	test.txt 파일에 아무 내용이나 적는다 한글,영어 소문자 대문자 섞어서 작성
	
	//test.txt의 내용을 읽어서
	//내용에 대문자와 소문자의 개수를 출력하시오
	
	//대문자 : 7
	//소문자 : 22

	int upper = 0;
	int lower = 0;

	한글, 특수문자 판단할 필요 없다.

	try{
	FileReader fr = new FileReader("D:/web14_lhj/test.txt");
	int code = 0;
		while((code = fr.read()) != -1) {
			if(code >= 'A'65 && code <= 'Z'96) {
				upper++;
			}

			if( code >='a' && code <='z') {
				lower++;
			}

		}//while
		System.out.println("대문자: " + upper);
		System.out.println("대문자: " + lower);

		fr.close();
	} catch(Exception e) {

	}
    }//main
}
```

### Ex2_FileWriter클래스 char기반의 출력스트림
```java
public class Ex3_FileWriter{
	public static void main(String[] args) {
   

		try{
		FileWriter fw = new FileWriter("D:/web14_lhj/fileWriter예제.txt");
		
		
		fw.write("첫번째 줄 작성합니다 hehehe".getBytes());
		fw.write("\n");
		fw.write("두번째 줄도 문제없지 hehehe");

		fw.close();

		} catch ( Exception e) {
			e.printStactTrace();
		}
	}
}


이제 ui쪽을 보면은 지금 우리 단계에서는 이미지파일을 전송할 수가 없다.
그래서 저랑  fileWriter 같은건 한번 더 보지 않을까 요런거는 생각을 하고 있고 나중에 이미지 같은거 업로드 해야되면 그땐 byte기반스트림을 써야한다..
하지만 바이트기반스트림으로 뭔가 업로드 하기 위한 준비가 다 되어있는 클래스를 가져다가 쓸것이다.
우리가 직접 만드는 그런 상황은 앞으로 그렇게 많이 나오지 않을것이다.
```
## 보조 스트림
- 스트림은 기능에 따라 스트림과 보조 스트림으로 구분한다.
    - 기반 스트림 : 대상에 직접 바료를 읽고 쓰는 스트림입니다.
    - 보조 스트림 : 직접 읽고 쓰는 기능 없이 기반 스트림에 추가로 사용할 수 있는 스트림이다.
 
- 보조 스트림은 실제로 데이터를 주고받을 수는 없다.
- 스트림의 기능을 향상시키거나 새로운 기능을 제공해주는 스트림으로 다른 보조스트림과 중첩하여 사용할 수 있다.

## 보조 스트림 연결하기
- 보조 스트림을 사용하려면 보조 스트림을 매개변수로 받는 기반 스트림이 먼저 선언되어야 한다.
- 보조 스트림은 스스로 데이터를 읽거나 쓸 수 없기 때문에 입출력과 바로 연결되는 기반 스트림이 필요하다.

```java
보조 스트림 변수명 = new 보조 스트림(기반 스트림);
```

## 성능 향상 보조 스트림
- 느린 하드디스크와 네트워크는 입출력 성능에 영향을 준다.
- 이때 입출력 소스와 직접 작업하지 않고 버퍼라는 메모리를 이용해 작업하면 실행 성능을 향상시킬 수 있다.
- 하지만 버퍼는 크기가 작아 많은 양의 데이터를 처리하기에는 부족하다.
- 보조 스트림 중에서는 다음과 같이 메모리 버퍼를 추가로 제공하여 스트림의 성능을 향상시키는 것들이 있다.
    - 바이트 기반 스트림: BufferedInputStream,BufferedOutputStream
    - 문자 기반 스트림 : BufferedReader,BufferedWriter

![image](https://github.com/to7485/Java1900/assets/54658614/a19f06db-01d8-42df-8dd0-71a1005067d5)

## Ex1_BufferedInput
```java
package test;

import java.io.BufferedInputStream;
import java.io.FileInputStream;

public class Test {
	public static void main(String[] args) {
			//보조스트림 사용
		FileInputStream in = null;
		BufferedInputStream bis = null;
		
		try {
			in = new FileInputStream("test.txt");
			bis = new BufferedInputStream(in);
			
			int read = 0;
			
			//보조 스트림을 사용하면 라인 단위로 읽어올 수 있다.
			while((read  = bis.read())!= -1) {
				System.out.print((char)read);
			}
		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if(bis != null) {
					bis.close();
				}
				if(in != null) {
					in.close();
				}
			} catch (Exception e2) {
				// TODO: handle exception
			}
		}
	}
}
```
## Ex2_ReadImage
- 보조 스트림 읽기 성능 테스트
```java
package test;

import java.io.BufferedInputStream;
import java.io.FileInputStream;

public class Test {
	public static void main(String[] args) {
		// 보조스트림 사용
		FileInputStream readFile = null;
		FileInputStream bisReadFile = null;
		BufferedInputStream bis = null;

		try {
			System.out.println("기본 스트림으로 읽기 시작");
			readFile = new FileInputStream("wall.jpg");
			// 현재 시간을 m/s 단위로 나타냄
			long start = System.currentTimeMillis();
			System.out.println("이미지 읽기 시작1");
			while (readFile.read() != -1) {
				// 이미지 읽기
			}
			System.out.println("이미지 읽기 종료1");
			long end = System.currentTimeMillis();
			long time = (end - start) / 1000;

			System.out.println("소요 시간 : " + time + "초");
			System.out.println("기본 스트림으로 읽기 종료");

			System.out.println("보조 스트림으로 읽기 시작");
			bisReadFile = new FileInputStream("wall.jpg");
			bis = new BufferedInputStream(bisReadFile);

			// 현재 시간을 m/s 단위로 나타냄
			start = System.currentTimeMillis();
			System.out.println("이미지 읽기 시작2");
			while (bis.read() != -1) {
				// 이미지 읽기
			}
			System.out.println("이미지 읽기 종료2");
			end = System.currentTimeMillis();
			double result = (end - start) / 1000;

			System.out.println("소요 시간 : " + result + "초");
			System.out.println("보조 스트림으로 읽기 종료");

		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if (bis != null) {
					bis.close();
				}
				if (bisReadFile != null) {
					bisReadFile.close();
				}
				if(readFile != null) {
					readFile.close();
				}
			} catch (Exception e2) {
				// TODO: handle exception
			}
		}
	}
}
```

## Ex3_CopyImage
- 보조 스트림을 이용한 이미지 복사
```java
package test;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;

public class Test {
	public static void main(String[] args) {
		FileInputStream readFile = null;
		BufferedInputStream bis = null;
		
		FileOutputStream writeFile = null;
		BufferedOutputStream bos = null;
		
		try {
			System.out.println("기본 스트림으로 복사 시작");
			readFile = new FileInputStream("wall.jpg");
			writeFile = new FileOutputStream("wall_copy.jpg");
			
			int read = 0;
			
			long start = System.currentTimeMillis();
			System.out.println("이미지 복사 시작1");
			while((read = readFile.read())!= -1) {
				writeFile.write(read);
			}
			System.out.println("이미지 복사 종료1");
			long end = System.currentTimeMillis();
			long time = (end - start)/10000;
			
			System.out.println("소요 시간 : " + time + "초");
			System.out.println("기본 스트림으로 복 종료");
			
			readFile.close();
			writeFile.close();
			
			System.out.println("보조 스트림으로 복사 시작");
			
			readFile = new FileInputStream("wall.jpg");
			writeFile = new FileOutputStream("wall_copy.jpg");
			
			bis = new BufferedInputStream(readFile);
			bos = new BufferedOutputStream(writeFile);
			
			start = System.currentTimeMillis();
			System.out.println("이미지 복사 시작2");
			while(bis.read() != -1) {
				//이미지 쓰기
				bos.write(read);
			}
			
			System.out.println("이미지 복사 종료2");
			end = System.currentTimeMillis();
			double result = (double)(end-start)/1000;
			
			System.out.println("소요 시간 : " + time+"초");
			System.out.println("보조 스트림으로 복사 종료");
			
	
		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if(bis != null) {
					bis.close();
				}
				if(readFile != null) {
					readFile.close();
				}
				
				if(bos != null) {
					bos.close();
				}
				if(writeFile != null) {
					writeFile.close();
				}
				
			} catch (Exception e2) {
				// TODO: handle exception
			}
			
		}
	}
}
```

## 문자 기반 보조 스트림
- BufferedReader는 Reader에 BufferedWriter는 Writer에 연결되어 버퍼를 제공해주는 보조스트림이다.
- 바이트 기반 스트림과 마찬가지로 보조 스트림을 사용해 성능을 향상시킬 수 있다.
- BufferedReader 또는 BufferedWriter의 경우, 버퍼에 데이터를 저장하여 입력 또는 출력하기 때문에 한 단어 뿐만 아니라 문장 단위로 데이터를 읽거나 쓸 수 있다.

### Ex1_BufferedReader
```java
package test;

import java.io.BufferedReader;
import java.io.FileReader;

public class Test {
	public static void main(String[] args) {
		FileReader reader = null;
		BufferedReader br = null;
		
		try {
			reader = new FileReader("book.txt");
			br = new BufferedReader(reader);
			
			//문장을 저장할 변수 
			String str = "";
			
			//버퍼에 문자를 저장하기 때문에 한번에 읽기 가능
			while((str = br.readLine())!= null) {
				System.out.println(str);
			}
		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if(br != null) {
					br.close();
				}
				if(reader != null) {
					reader.close();
				}
			} catch (Exception e2) {
				// TODO: handle exception
			}
		}
	}
}
```

### Ex2_BufferedWriter
```java
package test;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;

public class Test {
	public static void main(String[] args) {
		
		FileReader reader = null;
		BufferedReader br = null;
		
		FileWriter writer = null;
		BufferedWriter bw = null;
		
		try {
			reader = new FileReader("book.txt");
			writer = new FileWriter("book_copy.txt",false);
			
			br = new BufferedReader(reader);
			bw = new BufferedWriter(writer);
			
			//문장을 저장할 변수 
			String str = "";
			
			//버퍼에 문자를 저장하기 때문에 한번에 읽기 가능
			while((str = br.readLine())!= null) {
				bw.write(str+"\n");
			}
			System.out.println("텍스트 파일 복사 완료");
		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if(bw != null) {
					bw.close();
				}
				if(writer != null) {
					writer.close();
				}
				
				if(br != null) {
					br.close();
				}
				if(reader != null) {
					reader.close();
				}
			} catch (Exception e2) {
				// TODO: handle exception
			}
		}
	}
}
```

## 문자 변환 보조 스트림
- 바이트 기반 스트림으로 텍스트 파일을 읽거나 쓸 경우, 한글을 포함한 비영여권 문자들이 정상적으로 출력되지 않았다.
- 소스 스트림이 바이트 기반의 스트림이고, 입출력 데이터가 문자라면 Reader와 Writer로 변환하여 사용하는것을 고려해야 한다.
- 그 이유는 Reader와 Writer는 문자 단위로 입출력하기 때문에 바이트 기반 스트림보다 다양한 문자를 입출력할 수 있기 때문이다.

## InputStreamReader
- InputStreamReader는 바이트 기반 스트림 InputStream을 문자 기반의 스트림 Reader로 변환하는 보조 스트림이다.
```java
FileInputStream in = new ...
InputStreamReader is = new InputStreamReader(in);
InputStreamReader is = new InputStreamReader(in, text-encoding);
```
- InputStreamReader를 선언할 때는 text-encoding을 선택해 선언할 수 있다.
- 개발 환경의 text-encoding이 기본적으로 지정되어 사용된다.
- 만약 개발 환경이 읽어 들이는 파일의 text-encoding과 다르다면 직접 지정해야 한다.

### Ex1_InputStreamReader
```java
package test;

import java.io.FileInputStream;
import java.io.InputStreamReader;

public class Test {
	public static void main(String[] args) {
		
		FileInputStream in = null;
		InputStreamReader is = null;
		
		try {
			in = new FileInputStream("test.txt");
			is = new InputStreamReader(in,"UTF-8");
			int read = 0;
			
			while((read = is.read())!= -1) {
				System.out.println((char)read);
			}
		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if(is != null) {
					is.close();
				}
				if(in != null) {
					in.close();
				}
			} catch (Exception e2) {
				// TODO: handle exception
			}
		}
	}
}
```
- 바이트 기반 스트림으로 읽었지만 문자 변환 보조 스트림을 사용하여 변환함으로써 한글과 영문이 정상적으로 출력되었다.

## OutputStreamWriter
- OutputStreamWriter는 바이트 기반 스트림 OutputStream을 문자 기반의 스트림 Writer로 변환하는 보조스트림이다.

```java
FileOutputStream out = new ...;
OutputStreamWriter is = new OutputStreamWriter(out);
OutputStreamWriter is = new OutputStreamWriter(out,text-encoding);
```

### Ex1_OutputStreamReader
```java
package test;

import java.io.FileOutputStream;
import java.io.OutputStreamWriter;

public class Test {
	public static void main(String[] args) {
		
		FileOutputStream in = null;
		OutputStreamWriter is = null;
		
		try {
			in = new FileOutputStream("test.txt");
			is = new OutputStreamWriter(in,"UTF-8");
			
			System.out.println("파일 생성 시작");
			String[] strArray = {
					"OutputStreamWriter에 대해서 배웁니다."
					,"we are learning about OutputStreamWriter"};
			
			for(String str: strArray) {
				is.write(str+"\n");
			}
			System.out.println("파일 생성 완료");
		} catch (Exception e) {
			// TODO: handle exception
		} finally {
			try {
				if(is != null) {
					is.close();
				}
				if(in != null) {
					in.close();
				}
			} catch (Exception e2) {
				// TODO: handle exception
			}
		}
	}
}
```
## 보조스트림으로 입력받기
- BufferedReader를 통해 키보드에서 입력받기
- 장점 : Scanner보다 속도가 빠르다
```java
BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

문자열 입력받기
String str = reader.readLine();

정수 입력받기
int n = Integer.parseInt(reader.readLine());

특정 기준을 가지고 정수 여러개 입력받기
String[] arr = reader.readLine().split("");
System.out.println(Arrays.toString(arr));
```
