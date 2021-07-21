---
title: "[21.04.29] 초급JAVA스터디 - BufferedReader(StringTokenize) & BufferedWriter"
date: 2021-04-29 12:40:28 -0400
categories: Java_Study
---

# JAVA "BufferedReader(StringTokenize)" & "BufferedWriter"

아직 JAVA를 열심히 배우고 있는 초보라 BufferedReader랑 Writer를 사용하는 게 아직 많이 헷갈려서 자주 보면서 익히려고 따로 정리해 보기로 했다... !

~

**BufferedReader/BufferedWriter**는 이름처럼 **버퍼를 이용**해서 읽고 쓰는, Buffer에 있는 IO 클래스이다.      
입력된 데이터가 바로 전달되지 않고 중간에 버퍼링이 된 후에 전달되고, 출력도 마찬가지로 버퍼를 거쳐서 간접적으로 출력장치로 전달되기에 시스템의 데이터처리 효율성을 높여준다.       
또한 버퍼스트림을 InputStreamReader / OutputStreamWriter를 같이 사용하여 버퍼링을 하게 되면 입출력 스트림으로부터 미리 버퍼에 데이터를 갖다 놓기 때문에 보다 효율적인 입출력이 가능하다.       
이렇게 **_버퍼_** 를 이용하면 입출력의 효율이 비교할 수 없을 정도로 좋아지는 것!

한 번 거쳐가는 작업 때문에 오히려 느릴 것 같은데 왜 빠른 걸까.     
하드디스크는 원래 속도가 엄청 느리다.       
하드뿐만 아니라 키보드나 모니터와 같은 외부 장치와의 데이터 입출력은 생각보다 시간이 많이 걸리는 작업이다.        

버퍼 없이 키보드가 눌릴 때마다 눌린 문자의 정보를 목적지로 바로 이동시키는 것보다 중간에 메모리 버퍼를 두어서 데이터를 한번에 묶어서 이동시키는 것이 보다 효율적이고 빠르다. (그냥  전송하게 되면 CPU와 성능 갭이 많이 나서 비효율적이다.)        

즉, 흙을 파서 언덕에 버리는데, 한 번 삽질할 때마다 가서 버리는 것보다는 수레에 가득 채워서 한 번에 나르는 것이 효율적이라는 소리!  

### import 해야 할 항목들
> import java.io.BufferedReader;    
> import java.io.BufferedWriter;     
> import java.io.IOException;    
> import java.io.InputStreamReader;     
> import java.io.OutputStreamWriter;     
> import java.util.StringTokenizer;

## BufferedReader
나와 같은 Java에 익숙하지 않은 사람들이 주로 받는 입력방식은 **Scanner**이다. Scanner를 통해 입력을 받을 경우 `Space`, `Enter`를 모두 경계로 인식하기에 입력받은 데이터를 가공해야 하는 경우는 비교적 적고, 가공하기에도 매우 편리하다.         
하지만 그에 비해 BufferedReader는 `Enter`만 경계로 인식하고, 받은 데이터가 `String`으로 고정되기 때문에 입력받은 데이터를 가공하는 작업이 필요할 경우가 많다.

그래도!        
많은 양의 데이터를 입력받을경우 **BufferedReader**를 통해 입력받는 것이 **효율면**에서 훨씬 낫다는 거! 

### [BufferedReader 사용법]

	BufferedReader bf = new BufferedReader(new InputStreamReader(System.in)); //선언
	String s = bf.readLine(); //String
	int i = Integer.parseInt(bf.readLine()); //Int
	
 선언은 위에 있는 예제처럼 하면 된다. 입력은 readLine();이라는 메서드를 활용하면 되는데, 주의할점이 두가지가 있다.       
   
첫번째는 readLine()시 리턴값을 String으로 고정되기에 String이 아닌 다른타입으로 입력을 받을려면 형변환을 꼭 해주어야한다는 점이다.          
두번째로는 **예외처리** 를 꼭 해주어야 한다. readLine을 할때마다 try & catch를 활용하여 예외처리를 해주어도 되지만 대개 throws IOException을 통하여 작업한다.

### [Read한 데이터 가공]
	
 BufferedReader를 사용하여 Read한 데이터는 Line단위(한 줄 단위)로만 나눠지기에 **공백단위** 로 데이터를 가공하려면 따로 작업을 해주어야 한다.       
이에 대해서는 아래의 두가지 방법이 대표적이라고 할 수 있겠다.  
       
첫 번째 방법은 StringTokenizer에 nextToken()함수를 쓰는 것이다.      

	StringTokenizer st = new StringTokenizer(s); //StringTokenizer인자값에 입력된 문자열 넣는다.
		int a = Integer.parseInt(st.nextToken()); //첫번째 공백단위로 가공한 값 호출
		int b = Integer.parseInt(st.nextToken()); //두번째 공백단위로 가공한 값 호출

이렇게 nextToken함수에서 readLine()을 통해 입력받은 값을 공백단위로 구분하여 순서대로 호출할 수 있다.        

두 번째 방법으로는 String.split()함수를 활용하는 방식이 있다. 

	String array[] = s.split(" "); //공백마다 데이터 끊어서 배열에 넣음
	
이 함수를 이용하여 입력된 문자열을 공백단위로 끊어서 배열에 데이터를 넣고 사용하는 것이다.

## BufferedWriter
일반적으로 우리는 System.out.println("");을 이용하여 출력하곤 한다.     

사실 이를 대체할 수 있는 방법으로는, `StringBuilder` 로 하나의 문자열로 계속 연결시킨 뒤 가장 마지막에 연결된 하나의 문자열을 출력시키는 방법, 
그리고 `BufferedWriter` 로 버퍼에 담아둬았다가 한 번에 데이터를 보내는, 두 가지 방법이 있다.        

적은 양의 출력일 때는 성능 차이가 미미하지만, 많은 양의 데이터를 출력할 경우 System.out.println("");보다는 **BufferedWriter**를 통해 출력하는 것이 **효율면**에서 훨씬 낫다는 거! 

### BufferedWriter 사용법

	BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));//선언
	String s = "abcdefg";//출력할 문자열
	bw.write(s);//출력
	bw.newLine(); //줄바꿈
	bw.flush();//남아있는 데이터를 모두 출력시킴
	bw.close();//스트림을 닫음

BufferedWriter 의 경우 버퍼를 잡아 놓았기 때문에 flush() / close() 를 반드시 호출해 주어 뒤처리를 해주어야 한다. 그리고 bw.write에는 System.out.println();과 같이 자동개행기능이 없기 때문에 개행을 해주어야할 경우에는 `\n`를 통해 따로 처리해주어야 한다.

<img width="734" alt="스크린샷 2021-04-29 오후 12 21 38" src="https://user-images.githubusercontent.com/63195670/116498767-7e027700-a8e5-11eb-981e-be5c4b720eb4.png">

## 출처

[참고 글 링크 :)](https://coding-factory.tistory.com/251)
