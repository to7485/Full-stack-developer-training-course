# Stream
기존의 Java에서 컬렉션 데이터를 처리할 때 특정 조건에 따라 필터링을 하려면 복잡한 과정을 거쳐야 했다.

반면에 SQL문법의 경우 사용자가 원하는 조건의 데이터를 목록을 검색할 때 명시적이고 간단한 방법을<br>
이용했는데 Java8 에서 새로 추가된 기능인 스트림은 Java의 컬렉션 데이터에 대해 SQL 질의문 처럼<br>
데이터를 처리할 수 있는 기능을 가지고 있습니다.<br>

## Stream이란?

### 기존 루프문 처리의 문제점

기존 Java에서 컬렉션 데이터를 처리할때는 for, foreach 루프문을 사용하면서 컬렉션 내의 요소들을 하나씩 다루었습니다.<br>
간단한 처리나 컬렉션의 크기가 작으면 큰 문제가 아니지만 복잡한 처리가 필요하거나<br>
컬렉션의 크기가 커지면 루프문의 사용은 성능저하를 일으키게 되었습니다.<br>

### 스트림의 등장
스트림은 Java8에서 추가된 기능으로 컬렉션 데이터를 선언형으로 쉽게 처리할수 있습니다. 복잡한 루프문을

사용하지 않아도 되며 루프문을 중첩해서 사용해야 되는 최악의 경우도 더이상 없어졌습니다.

스트림은 '데이터의 흐름'입니다. 배열 또는 컬렉션 객체에 함수 여러개를 조합해서 원하는 결과를 필터링하고 가공된 결과를 얻을 수 있습니다.<br>
또한 람다식을 이용해서 코드의 양을 줄이고 간결하게 표현할 수 있습니다. <br>
즉, 배열과 컬렉션을 함수형으로 처리할 수 있습니다.<br>

### 스트림의 특징
- 스트림은 데이터 소스로 부터 데이터를 읽기만 할 뿐, 데이터 소스를 변경하지 않는다.
- 스트림은 한번 사용하면 닫혀서 다시 사용할 수 없다.(다시 사용하려면 스트림을 다시 생성해야 한다.)
```
strStream1.sorted().forEach(x -> System.out.println(x));
int numOfStr = strStream1.count(); // 스트림이 닫혔으므로 에러 발생 
```

- 스트림은 작업을 내부 반복으로 처리한다.
```
void forEach(Consumer<? super T> action) {
	Objects.requireNonNull(action); // 매개변수의 널 체크
	
	for(T t : src) {
		action.accept(T);
	}
}
```
## 스트림 사용 과정
1. 생성하기 : 스트림 객체 생성
2. 가공하기 : 필터링(filtering) 및 맵핑(mapping)등 원하는 결과를 만들어가는 중간작업
3. 결과만들기 : 최종적으로 결과를 만들어내는 작업


## 스트림 객체 생성
보통 배열과 컬렉션을 이용해서 스트림을 만들지만 이 외에도 다양한 방법으로 스트림을 만들수 있다.

### 배열을 통한 생성
- Arrays 클래스 -> static stream()
- Stream.of(T[] t)
- Stream.of(T...values)
```
Stream<T> Stream.of(T... values) // 가변인자
Stream<T> Stream.of(T[])
Stream<T> Arrays.stream(T[])
Stream<T> Arrays.stream(T[] array, int startInclusive, int endExclusive)  // startInclusive이상 endExclusive 미만 범위의 스트림 생성
```
```
사용 예)
Stream<String> strStream = Stream.of("a", "b", "c"); // 가변인자
Stream<String> strStream = Stream.of(new String[] {"a", "b", "c"});
Stream<String> strStream = Arrays.stream(new String[]{"a", "b","c"});
Stream<String> strStream = Arrays.stream(new String[]{"a", "b", "c", "d"}, 0, 3);
```

int, long, double과 같은 기본형 배열을 소스로 하는 스트림을 생성하는 메서드

```
IntStream IntStream.of(int... values)
IntStream IntStream.of(int[])
IntStream Arrays.stream(int[])
IntStream Arrays.stream(int[] array, int startInclusive, inbt endExclusive) // startInclusive이상 endExclusive 미만 범위의 스트림 생성
```

![image](https://user-images.githubusercontent.com/54658614/225211207-6d063c3c-8a79-43cb-9643-a5cb12a816b3.png)

#### Ex1_stream 클래스 생성

```java
package ex1_stream;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.stream.IntStream;
import java.util.stream.Stream;

public class Ex1_stream {
	public static void main(String[] args) {
		String[] strArray = {"홍길동","신용권","김미나"};
		Stream<String> strStream = Arrays.stream(strArray);
		strStream.forEach(item -> System.out.print(item+","));
		System.out.println();
		
		int[] intArray = {1,2,3,4,5};
		IntStream intStream = Arrays.stream(intArray);
		intStream.forEach(item -> System.out.print(item+","));
		System.out.println();
	}
}
```

### 컬렉션을 통한 생성
- 컬렉션 타입(Collection,List,Set)의 경우 인터페이스에 추가된 디폴트 메서드 stream을 이용해서 스트림을 만들 수 있다.

```
모든 컬렉션 프레임워크의 조상인 Collection 인터페이스에 default 메서드로 되어있다.
public interface Collection<E> extends Iterable<E> {
  default Stream<E> stream() {
    return StreamSupport.stream(spliterator(), false);
  } 
  // ...
}
```

https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/stream/Stream.html

```
List<Integer> list = Arrays.asList(1,2,3,4,5);
Stream<Integer> intStream = list.stream();
intStream.forEach(i -> System.out.println(i));  // 또는 메서드 참조 방식으로 람다식 정의 intStream.forEach(System.out::println);
```

#### Ex2_stream 클래스 생성
```java
package test;
import java.util.HashSet;
import java.util.Set;
import java.util.stream.Stream;

public class Test{
	public static void main(String[] args) {

		//Set 컬렉션 생성
		Set<String> set = new HashSet<>();
		set.add("홍길동");
		set.add("신용권");
		set.add("김미나");
		
		//Stream을 이용한 요소 반복 처리
		Stream<String> stream = set.stream();
		stream.forEach(System.out::println);
		
		//Stream은 Iterator와 비슷한 반복자이지만, 다음과 같은 차이점을 가지고 있다.
		//1) 내부 반복자이므로 처리 속도가 빠르고 병렬처리에 효율적이다.
		//2) 람다식으로 다양한 요소 처리를 정의할 수 있다.
		//3) 중간 처리와 최종 처리를 수행하도록 파이프 라인을 형성할 수 있다.

		ArrayList<String> names = new ArrayList<String>();
		names.add("홍길동");
		names.add("신용권");
		names.add("김자바");
		names.add("람다식");
		names.add("김미나");
		
		Stream<String> stream = names.stream();
		stream.forEach(System.out::println);
		
		stream.forEach(System.out::println);
	}
}
```

![image](https://user-images.githubusercontent.com/54658614/225211299-91e01eb1-70c0-4d81-9bea-167bc31f9479.png)

### 기본타입형 스트림   
 ![image](https://user-images.githubusercontent.com/54658614/225215406-7d544837-ea30-49c3-938a-197445713d7b.png)

- 요소의 타입이 T인 스트림은 기본적으로 Stream<T>인데, 기본 자료형을 다루려면 오토박싱&언박싱이 발생하여 비효율성이 증가한다(예 - Integer <-> int)
- 비효율성을 줄이기 위해 데이터 소스의 요소를 기본형으로 다루는 스트림이 제공된다.
- IntStream, LongStream, DoubleStream
- 기본자료형에 유용하게 사용할 수 있는 메서드를 제공한다.
	
![image](https://user-images.githubusercontent.com/54658614/225210056-42f96d3e-368a-456e-a586-73be73e09b33.png)
	
#### Ex3_stream 클래스 생성

```java
package test;

import java.util.stream.IntStream;

public class Test{
	public static void main(String[] args) {

		//특정 범위의 정수를 요소로 갖는 스트림 생성하기
		IntStream intStream1 = IntStream.range(1, 5); // 1,2,3,4
		IntStream intStream2 = IntStream.rangeClosed(1, 5); // 1,2,3,4,5

		//난수를 요소로 갖는 스트림 생성하기
		IntStream intStream3 = new Random().ints(); // 무한 스트림
		intStream3.limit(5).forEach(System.out::println); // 5개의 요소만 출력한다.

		IntStream intStream4 = new Random().ints(5); // 크기가 5인 난수 스트림을 반환
	
		int total = 0;
		for(int i = 1; i <= 10; i++) {
			total += i;
		}
		System.out.printf("1~10까지의 합 : %d\n",total);
		
		int total2 = IntStream.rangeClosed(1, 10).sum();
		System.out.printf("1~10까지의 합 : %d\n",total2);


	}
}
```

### 람다식을 소스로 하는 스트림 생성하기
```java
▶ 람다식을 소스로 하는 스트림 생성하기
static <T> Stream<T> iterate(T seed,UnaryOperator<T> f) // 이전 요소에종속적 
static <T> Stream<T> generate(Supplier<T> s) // 이전 요소에 독립적

Stream<Integer> evenStream = Stream.iterate(0, n->n+2); // 0,2,4,6, ...
Stream<Double> randomStream = Stream.generate(Math::random);
Stream<Integer> oneStream = Stream.generate(()->1);
```

## 스트림의 연산
### 중간연산 
연산 결과가 스트림인 연산, 스트림에 연속해서 중간 연산할 수 있다.

#### 스트림의 중간 연산 목록 
- 연산의 결과가 스트림이면 중간연산

|중간 연산|설명|
|----------|-------|
|Stream\<T\> distinct()|중복을 제거|
|Stream\<T\> filter(Predicate\<T\> predicate)|조건에 안 맞는 요소 제외|
|Stream\<T\> limit(long maxSize)|스트림의 일부를 잘라낸다|
|Stream\<T\> skip(long n)|스트림의 일부를 건너뛴다|
|Stream\<T\> peek(Consumer\<T\> action)|스트림의 요소에 작업 수행|
|Stream\<T\> sorted()<br>Stream\<T\> sorted(Comparator\<T\> comparator)|스트림의 요소를 정렬한다.|
|Stream\<R\> map(Function\<T,R\> mapper)<br>DoubleStream mapToDouble(ToDoubleFunction\<T\> mapper)<br>IntStream mapToInt(ToIntFunction\<T\> mapper)<br><br>Stream\<R\> flatMap(Function\<T, Stream\<R\>\> mapper)<br>DoubleStream flatMapToDouble(Function\<T, DoubleStream\> m)<br>IntStream flatMapToInt(Function\<T, IntStream\> m)<br>LongStream flatMapToLong(Function\<T, LongStream\> m)|스트림의 요소를 변환한다.|

### 정렬 - sorted()
```
Stream<T> sorted()
Stream<T> sorted(Comparator<? super T> comparator)
```
Comparator를 지정하지 않으면 스트림 요소의 기본 정렬 기준(Comparable)으로 정렬한다. 단, 스트림의 요소가 Comparable을 구현한 클래스가 아니면 예외가 발생한다.

```
Stream<String> strStream = Stream.of("dd", "aaa", "CC", "cc", "b");
strStream.sort().forEach(System.out::println); 
```

### 스트림 자르기 - skip(), limit()
```
Stream<T> skip(long n)   // n만큼 건너뛰기
Stream<T> limit(long maxSize) // maxSize 만큼 자르기
```
```
IntStream intStream = IntStream.rangeClosed(1, 10); // 1~10의 요소를 가진 스트림
intStream.skip(3).limit(5).forEach(System.out::println); // 45678
```

### 스트림 요소 걸러내기 - filter(), distinct()
- filter() - 주어진 조건(Predicate)에 맞지 않는 요소를 걸러낸다.
- distinct() - 스트림에서 중복된 요소를 제거
```
Stream<T> filter(Predicate<? super T> predicate)
Stream<T> distinct()
```

- distinct() 
```
IntStream intStream = IntStream.of(1, 2, 2, 3, 3, 4, 5, 5, 6);
intStream.distinct().forEach(System.out::print); // 123456
```

- filter()
```
IntStream intStream = IntStream.rangeClosed(1, 10); // 1 ~ 10
IntStream.filter( i -> i % 2 == 0).forEach(System.out::print); // 246810
```
#### Ex4_stream 클래스 생성
```java
package ex1_stream;

import java.util.Arrays;
import java.util.stream.IntStream;
import java.util.stream.Stream;

public class Ex1_Stream {
	public static void main(String[] args) {
		Integer[] nums = {1,44,33,21,36,68,88,4,5,6,1,1,1,2,2,2};
		
		//1. 스트림 객체 생성
		Stream<Integer> stream =  Arrays.stream(nums);
		
		//2. 스트림에 중간연산
		stream.distinct()
			  .sorted()
			  .limit(5)
			  .forEach(System.out::println);
		
		//skip()
		//rangeClosed() : 정수 범위를 생성
		IntStream intStream = IntStream.rangeClosed(1, 10);
		intStream.skip(3).limit(5).forEach(x-> System.out.print(x+" "));
		
		System.out.println();

		//filter()
		IntStream inStream2 = IntStream.of(1,2,2,3,3,4,5,5,6,7,8,9,10);
		inStream2.distinct().filter(x -> x % 2 == 0).forEach(x -> System.out.print(x+" ")); //2 4 6 8 10
		
		System.out.println();
		//문자열의 길이가 3이상인 문자열만 출력
		Stream.of("ab","a","abc","abcd","abcdef","abcdefg").filter(x -> x.length() > 2).forEach(x-> System.out.print(x+" "));
	
	}
}
```
#### Student 클래스 생성
```java
package test;

import java.util.stream.Stream;

public class Student implements Comparable<Student>{
	String name;
	int ban;
	int totalScore;
	Student(String name, int ban, int totalScore) {
		this.name = name;
		this.ban = ban;
		this.totalScore = totalScore;
	}
	
	@Override
	public String toString() {
		return String.format("[%s, %d, %d]", name, ban, totalScore).toString();
	}
	
	String getName() { return name; }
	int getBan() { return ban; }
	int getTotalScore() { return totalScore; }
	
	@Override
	public int compareTo(Student s) {//성적이 높은 순으로 정렬
		return s.totalScore - this.totalScore;
	}
}
```
#### StudentMain 클래스 생성
```java
package test;

import java.util.Comparator;
import java.util.stream.Stream;

public class StudentMain {
	public static void main(String[] args) {
		Student[] students = {
				new Student("이자바", 3, 300),
				new Student("김자바", 1, 200),
				new Student("안자바", 2, 100),
				new Student("박자바", 2, 150),
				new Student("소자바", 1, 200),
				new Student("나자바", 3, 290),
				new Student("강자바", 3, 180)	
		};
	
		Stream.of(students).sorted(Comparator.comparing(Student::getBan)// 반별 정렬
				.thenComparing(Student::getTotalScore)).forEach(System.out::println); 
				//성적순 정렬	
	}
}

```
comparing메서드의 반환형이 Comparator<T>라서 뒤에 더 조건을 달 수 있는 것

![image](https://user-images.githubusercontent.com/54658614/225517289-4b2ad218-6f32-4242-818c-dbf859b5b3ec.png)

조건을 더 달 때는 thenComparing을 사용한다.

![image](https://user-images.githubusercontent.com/54658614/225517908-6a3e2e89-d28b-43dc-855c-3ef5e0e99344.png)

thenComparing은 파라미터로 Function을 가지고 있고 Function은 apply 메서드를 가지고 있다.

![image](https://user-images.githubusercontent.com/54658614/225517967-f77bc62f-83e5-4d63-91de-5d7f666eb73b.png)


### 최종연산
- 연산 결과가 스트림이 아닌 연산.
- 스트림의 요소를 소모하므로 단 한번만 가능

```
stream.distinct().limit(5).sorted().forEach(x -> System.out.println(x));
      
distinct(), limit(5), sorted() - 중간연산
forEach - 최종연산
```

#### 스트림의 최종 연산 목록
- 연산의 결과가 스트림이 아니면 최종연산

|최종 연산|설명|
|----------|-------|
|void forEach(Consumer\<? super T\> action)|void forEachOrdered(Consumer\<? super T\> action)|각 요소에 지정된 작업 수행|
|long count())|스트림의 요소의 개수 반환|
|Optional\<T\> max(Comparator\<? super T\> comparator)<br>Optional\<T\> min(Comparator\<? super T\> comparator)|스트림의 최대값/최소값을 반환|
|Optional\<T\> findAny() // 아무거나 하나<br>Optional\<T\> findFirst() // 첫 번째 요소|스트림의 요소를 하나 반환|
|boolean allMatch(Predicate\<T\> p) // 모두 만족하는지<br>boolean anyMatch(Predicate\<T\> p) // 하나라도 만족하는지<br>boolean noneMatch(Predicate\<T\> p) // 모두 만족하지 않는지|주어진 조건을 모든 요소가 만족시키는지, 만족시키지 않는지 확인|
|Object[] toArray()<br>A[] toArray(IntFunction\<A[]\> generator)|스트림의 모든 요소를 배열로 변환|
|Optional\<T\> reduce(BinaryOperator\<T\> accumulator)<br>T reduce(T identity, BinaryOperator\<T\> accumulator)|스트림 요소를 하나씩 줄여가면서(리듀싱) 계산한다.|
|R collect(Collector\<T,A,B\> collector)|스트림의 요소를 수집한다.<br>주로 요소를 그룹화하거나 분할한 결과를 컬렉션에 담아 반환하는데 사용한다.|

### forEach(),forEachOrdered()
- 스트림의 모든 요소에 지정된 작업을 수행

#### Ex5_stream 클래스 생성
```java
package test;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.stream.Stream;

public class Test{
	public static void main(String[] args) {

		int[] nums = {1,44,33,21,35,67,99,4,5,6,1,1,1,2,2,2};
		Arrays.stream(nums).distinct().sorted().limit(5).forEach(System.out::println);
	}
}
```

#### Ex6_stream 클래스 생성
```java
package test;


import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.stream.Collectors;

public class Test{
	public static void main(String[] args) {

		//List 컬렉션 생성
		ArrayList<String> list1 = new ArrayList<>();
		list1.add("홍길동");
		list1.add("신용권");
		list1.add("감자바");
		list1.add("람다식");
		list1.add("박병렬");
		
		//Collections.sort(list1);
		//System.out.println(list1);
		
		
		//Collectors란 "stream을 일반적인 List,Set등으로 변경시키는 Stream메서드)
		//toCollection()을 이용하여 좀 더 특정한 컬렉션으로 구현이 가능하다.
		ArrayList<String>list1_1 = list1.stream().sorted().collect(Collectors.toCollection(ArrayList::new));
		System.out.println(list1_1);
		
		//배열 
		String[] list2 = {"홍길동","신용권","감자바","람다식","박병령"};
		
		//Arrays.sort(list2);
		//System.out.println(Arrays.toString(list2));
		
		String[] list2_1 = Arrays.stream(list2).sorted().toArray(String[]::new);
		System.out.println(Arrays.deepToString(list2_1));
		
		
	}
}

```
#### Ex7_stream 클래스 생성
```java
package test;

import java.util.Arrays;
import java.util.stream.Stream;

public class Test{
	public static void main(String[] args) {

		Integer[] nums = {1,2,3,4,5,6,7,8,9,10};
		
		Stream<Integer> stream = Arrays.stream(nums);
		int total = stream.reduce(0,(x,y)->x+y);
	}
}

```
![image](https://user-images.githubusercontent.com/54658614/225209478-ee701e04-1dd7-4034-8e32-22202a7fa318.png)

#### Ex8_stream 클래스 수정하기
				      
```java
package test;

import java.util.Arrays;
import java.util.stream.IntStream;

public class Test{
	public static void main(String[] args) {

		//Integer클래스
//		Integer[] nums = {1,2,3,4,5,6,7,8,9,10};
		int[] nums = {1,2,3,4,5,6,7,8,9,10};
		
//		Stream<Integer> stream = Arrays.stream(nums);
//		int total = stream.reduce(0,(x,y)->x+y);//기본자료형으로 바꿔줘야 해서 언박싱이 발생한다.
//		System.out.println(total);
		
		IntStream stream = Arrays.stream(nums);
		int total = stream.reduce(0, (x,y)->x+y);//기본자료형이기 때문에 언박싱이 일어나지 않는다.
		System.out.println(total);
	}
}

```
- 제네릭을 사용하지 않기 때문에 불필요한 오토박싱(auto-boxing)이 일어나지 않습니다.


- 지정된 범위의 난수를 발생시키는 스트림을 얻는 메서드
```
begin이상 end 미만 범위에서 난수 발생
IntStream  ints(int begin, int end)
LongStream longs(long begin, long end)
DoubleStream doubles(double begin, double end)
IntStream ints(long streamSize, int begin, int end)
LongStream longs(long streamSize, long begin, long end)
DoubleStream doubles(long streamSize, double begin, double end)
```
	
```
IntStream intStream = IntStream.range(1,5); //[1,2,3,4]
LongStream longStream = LongStream.rangeClosed(1,5); // [1,2,3,4,5]
```

### 임의의 수
Random 클래스에는 난수들로 이루어진 스트림을 반환하는 메서드를 가지고 있다.
```
IntStream ints()
LongStream longs()
DoubleStream doubles()
```
- 매개변수가 없다면 크키가 정해지지 않은 무한 스트림
- limit()를 함께 사용해서 스트림의 크기를 제한해 줘야 한다.
```
IntStream intStream = new Random().ints(); // 무한 스트림
intStream.limit(5).forEach(System.out::println); // 5개의 요소만 출력
```

- 매개변수가 있다면 크기가 정해진 유한스트림, limit()를 사용하지 않아도 된다.
```
IntStream ints(long streamSize)
LongStream longs(long streamSize)
DoubleStream doubles(long streamSize)
```

```
IntStream intStream = new Random().ints(5); // 크키가 5인 난수 스트림 반환
```
	
#### Ex9_stream 클래스 수정하기
```java
package test;

import java.util.Random;
import java.util.stream.IntStream;

public class Test{
	public static void main(String[] args) {

//		Random rnd = new Random();
//		IntStream stream = rnd.ints();
//		stream.limit(6).forEach(System.out::println);
		
		Random rnd = new Random();
		IntStream stream = rnd.ints(1,46); //범위 정하기
		stream.limit(6).forEach(System.out::println);
	}
}
```

### 람다식 - iterate(), generate()
람다식을 매개변수로 받아서 람다식에 의해 계산되는 값들을 요소로 하는 무한 스트림을 생성

```
static <T> Stream<T> iterate(T seed, UnaryOperator<T> f)
static<T> Stream<T> generate(Supplier<T> s)
```
- iterate()는 이전 결과를 이용해서 다음요소를 계산 
```
Stream<Integer> evenStream = Stream.iterate(0, n->n+2); // 0, 2, 4, 6 ... 
```
![image](https://user-images.githubusercontent.com/54658614/225216473-2bf9aad5-cb24-4cef-97c6-f6ec33527936.png)


- generate()는 이전 결과를 사용하지 않고 람다식에 의해 계산되는 값을 요소로 하는 무한 스트림을 생성하여 반환
- generate()는 이전 결과를 사용하지 않으므로 매개변수 타입이 Suppiler<T> 이다. 

```
Stream<Double> randomStream = Stream.generate(Math::random);
Stream<Integer> oneStream = Stream.generate(() -> 1);
```
#### Ex10_stream 클래스 생성
```java
package test;

import java.util.Arrays;
import java.util.stream.IntStream;

public class Test{
	public static void main(String[] args) {

		int[] nums = IntStream.iterate(1, x->x*2).limit(10).toArray();
		System.out.println(Arrays.toString(nums));
		
							//0~100 사이의 난수
		int[] nums2 = IntStream.generate(() ->(int)(Math.random()*101)).limit(10).toArray();
		System.out.println(Arrays.toString(nums2));
	}
}

```
	
### 빈 스트림
- 요소가 하나도 없는 비어있는 스트림 
- 스트림에서 연산을 수행한 결과가 하나도 없을 때, null 보다 빈 스트림을 반환하는 것이 좋다.
```
Stream emptyStream = Stream.empty(); // 빈 스트림을 생성해서 반환 
long count = emptyStream.count(); // count의 값은 0
```

### 두 스트림의 연결 - concat()
```
String[] str1 = {"123", "456", "789"}
String[] str2 = {"ABC", "abc", "DEF"};
Stream<String> strs1 = Stream.of(str1);
Stream<String> strs2 = Stream.of(str2);
Stream<String> strs3 = Stream.concat(strs1, strs2); 
```
#### Ex11_stream 클래스 생성
```java
package test;

import java.util.stream.Stream;

public class Test{
	public static void main(String[] args) {
		String[] str1 = {"123","456","789"};
		String[] str2 = {"abc","def","ghi"};
		
		Stream<String> str3 = Stream.of(str1);
		Stream<String> str4 = Stream.of(str2);
		
		Stream<String> str5 = Stream.concat(str3, str4);
		str5.forEach(x -> System.out.print(x+" "));
	}
}
```

### 변환 - map()
스트림의 요소에서 저장된 값 중에서 원하는 필드만 뽑아내거나 특정 형태로 변환해야 하는 경우
```
Stream<R> map(Function<? super T, ? extends R> mapper)
```

```
Stream<File> fileStream = Stream.of(new File("Ex1.java"), new File("Ex1"), new File("Ex1.bak"), 
new File("Ex2.java"), new File("Ex1.txt"));
// map()으로 Stream<File>을 Stream<String>으로 변환
Stream<String> filenameStream = fileStream.map(File::getName);
filenameStream.forEach(System.out::println); // 스트림의 모든 파일이름을 출력
```

### 변환 - map()
스트림의 요소에서 저장된 값 중에서 원하는 필드만 뽑아내거나 특정 형태로 변환해야 하는 경우
```
Stream<R> map(Function<? super T, ? extends R> mapper)
```

#### StudentMain에 코드 추가하기
```java
package test;

import java.util.Comparator;
import java.util.stream.Stream;

public class StudentMain {
	public static void main(String[] args) {
		Student[] students = {
				new Student("이자바", 3, 300),
				new Student("김자바", 1, 200),
				new Student("안자바", 2, 100),
				new Student("박자바", 2, 150),
				new Student("소자바", 1, 200),
				new Student("나자바", 3, 290),
				new Student("강자바", 3, 180)	
		};
	
		Stream.of(students).sorted(Comparator.comparing(Student::getBan)// 반별 정렬
				.thenComparing(Student::getTotalScore)).forEach(System.out::println); 
				//성적순 정렬

		System.out.println();

		//Students스트림을 score스트림으로 변환하고 점수를 콘솔에 출력하기
		Stream.of(students).mapToInt(x -> x.getTotalScore()).forEach(score -> System.out.println(score));
	}
}
```

```
### flatMap() - Stream<T[]>를 Stream<T>로 변환
스트림의 타입이 Stream<T[]>인 경우 Stream<T>로 변환해 준다.
```
Stream<String> strStrm = Stream.of("abc", "def", "jklmn");
Stream<String> strStrm2 = Stream.of("ABC", "GHI", "JKLMN");
Stream<Stream<String>> strmStrm = Stream.of(strStrm, strStrm2);
Stream<String> strStream = strmStrm.map(s -> s.toArray(String[]::new)) // Stream<Stream<String>> -> Stream<String[]>
												.flatMap(Arrays::stream); // Stream<String[]> -> Stream<String>
```
#### Ex12_stream 클래스 생성
```java
package day19;
import java.util.*;
import java.util.stream.*;
public class StreamEx4 {
	public static void main(String[] args) {
		Stream<String[]> strArrStrm = Stream.of(
				new String[] {"abc", "def", "jkl"},
				new String[] {"ABC", "GHI", "JKL"}
		);
		// Stream<Stream<String>> strStrmStrm = strArrStrm.map(Arrays::stream);
		Stream<String> strStrm = strArrStrm.flatMap(Arrays::stream);
		
		strStrm.map(String::toLowerCase)
			.distinct()
			.sorted()
			.forEach(System.out::println);
		System.out.println();
		
		String[] lineArr = {
				"Believe or not It is true",
				"Do or do not There is no try",
		};
		
		Stream<String> lineStream = Arrays.stream(lineArr);
		lineStream.flatMap(line -> Stream.of(line.split(" +")))
			.map(String::toLowerCase)
			.distinct()
			.sorted()
			.forEach(System.out::println);
		System.out.println();
		
		Stream<String> strStrm1 = Stream.of("AAA", "ABC", "bBb", "Dd");
		Stream<String> strStrm2 = Stream.of("bbb", "aaa", "ccc", "dd");
		
		Stream<Stream<String>> strStrmStrm = Stream.of(strStrm1, strStrm2);
		Stream<String> strStream = strStrmStrm
						.map(s -> s.toArray(String[]::new))
						.flatMap(Arrays::stream);
		strStream.map(String::toLowerCase)
			.distinct()
			.forEach(System.out::println);
	}
}
```
- 실행결과
```
abc
def
ghi
jkl
believe
do
is
it
no
not
or
there
true
try
aaa
abc
bbb
dd
ccc
```
## Optional<T>와 OptionalInt
- Optional<T>은 제네릭 클래스로 "T타입의 객체"를 감싸는 래퍼 클래스이다.
- Optional 타입의 객체에는 모든 타입의 참조변수를 담을 수 있다.
- 보통 값이 없을 때를 처리하기 위해 사용한다.
```
public final class Optional<T> {
	private final T value;  // T 타입의 참조변수
	...
}
```
- 스트림에서 최종연산의 결과를 Optional 객체에 담아서 반환
- 객체에 담아서 반환을 하므로 결과가 null인지를  간단하게 체크하는 메서드를 제공한다.
- if로 따로 체크하지 않아도 NullPointException이 발생하지 않는 보다 간결하고 안전한 코드 작성이 가능해 진다.

### Optional 객체 생성하기
- of() 또는 ofNullable()을 사용 
- 참조변수의 값이 null일 가능성이 있으면 of()대신 ofNullable()을 사용해야 한다.
- Optional<T>타입의 참조 변수를 기본값으로 초기화 할때는 empty()를 사용한다.
```
String str = "abc";
Optional<String> optVal = Optional.of(str);
Optional<String> optVal = Optional.of("abc");
Optional<String> optVal = Optional.of(new String("abc"));
```
```
Optional<String> optVal = Optional.of(null); // NullPointException 발생
Optional<String> optVal = Optional.ofNullable(null);//null값이 있을 때도 있으니 주의해라
```
```
Optional<String> optVal = Optional.<String>empty(); // 빈 객체로 초기화
```
### Optional 객체의 값 가져오기
- get()을 사용하여 Optional 객체에 저장된 값을 가져온다. 값이 null일 때는 NoSuchElementException이 발생한다.
- orElse("기본값")을 사용하면 값이 null일때 "기본값"으로 대체할 수 있다.
- 람다식을 매개변수로 하여 저장된 값을 가져올 수 있다.
```
T orElseGet(Supplier<? extends T> other)
T orElseThrow(Supplier<? extends X> exceptionSupplier)
```
```
String str3 = optVal2.orElseGet(String::new);
String str4 = optVal2.orElseThrow(NullPointerException::new);
```
### OptionalInt, OptionalLong, OptionalDouble
- IntStream과 같은 기본형 스트림에는 Optional도 기본형을 값으로 하는 OptionalInt, OptionalLong, OptionalDouble을 반환한다. 
- IntStream에 정의된 메서드 예
```
OptionalInt findAny()
OptionalInt findFirst()
OptionalInt reduce(IntBinaryOperator op)
OptionalInt max()
OptionalInt min()
OptionalDouble average()
```
- 반환타입이 Optional<T>가 아니라는 것을 제외하고는 Stream에 정의된 것과 비슷하나 Optional에 저장된 값을 꺼낼 때 사용하는 메서드의 이름이 조금씩 다르다

|Optinal클래스|값을 반환하는 메서드|
|-------|---------|
|Optional<T>|T get()|
|OptionalInt|int getAsInt()|
|OptionalLong|long getAsLong()|
|OptionalDouble|double getAsDouble()|

#### Ex13_stream 클래스 생성
```java
package day19;
import java.util.*;
public class OptionalEx1 {
	public static void main(String[] args) {
		Optional<String> optStr = Optional.of("abcde");
		Optional<Integer> optInt = optStr.map(String::length);
		System.out.println("optStr=" + optStr.get());
		System.out.println("optInt=" + optInt.get());
		
		int result1 = Optional.of("123")
						.filter(x->x.length() > 0)
						.map(Integer::parseInt).get();
		
		int result2 = Optional.of("")
						.filter(x->x.length() > 0)
						.map(Integer::parseInt).orElse(-1);
		
		System.out.println("result1=" + result1);
		System.out.println("result2=" + result2);
		
		Optional.of("456").map(Integer::parseInt)
				.ifPresent(x->System.out.printf("result3=%d%n", x));
		
		OptionalInt optInt1 = OptionalInt.of(0); // 0을 저장
		OptionalInt optInt2 = OptionalInt.empty(); // 빈 객체를 생성
		
		System.out.println(optInt1.isPresent()); // true
		System.out.println(optInt2.isPresent()); // false;
		
		System.out.println(optInt1.getAsInt()); // 0
		// System.out.println(optInt2.getAsInt()); // NoSuchElementException
		System.out.println("optInt1=" + optInt1);
		System.out.println("optInt2=" + optInt2);
		System.out.println("optInt1.equals(optInt2)?" + optInt1.equals(optInt2)); // false
		
		Optional<String> opt = Optional.ofNullable(null); // null을 저장
		Optional<String> opt2 = Optional.empty(); // 빈 객체를 생성
		System.out.println("opt = " + opt);
		System.out.println("opt2 = " + opt2);
		System.out.println("opt.equals(opt2)?" + opt.equals(opt2)); // true
		
		int result3 = optStrToInt(Optional.of("123"), 0);
		int result4 = optStrToInt(Optional.of(""), 0);
		
		System.out.println("result3=" + result3);
		System.out.println("result4=" + result4);
	}
	
	static int optStrToInt(Optional<String> optStr, int defaultValue) {
		try {
			return optStr.map(Integer::parseInt).get();
		} catch (Exception e) {
			return defaultValue;
		}
	}
}
```
- 실행결과
```
optStr=abcde
optInt=5
result1=123
result2=-1
result3=456
true
false
0
optInt1=OptionalInt[0]
optInt2=OptionalInt.empty
optInt1.equals(optInt2)?false
opt = Optional.empty
opt2 = Optional.empty
opt.equals(opt2)?true
result3=123
result4=0
```
## 스트림의 최종 연산
- 최종 연산은 스트림의 요소를 소모해서 결과를 
- 최종 연산후에는 스트림이 닫히게 되고 더 이상 사용할 수 없다.

### forEach()
- forEach()는 peek()와 달리 스트림의 요소를 소모하는 최종연산이다
- 반환 타입이 void이므로 스트림의 요소를 출력하는 용도로 사용된다.

```
void forEach(Consumer<? super T> action)
```

### 조건 검사 - allMatch(), anyMatch(), noneMatch(), findFirst(), findAny()
- allMatch() : 지정된 조건에 모든 요소가 일치하는지
- anyMatch() : 지정된 조건에 일부 요소가 일치하는지
- noneMatch() : 지정된 조건에 어떤 요소도 일치하지 않는지 
- findFirst() : 지정된 조건에 일치하는 첫 번째 것을 반환
- findAny() : 지정된 조건에 일치하는 첫 번째 것을 반환(병렬 스트림에서 사용)

```
boolean allMatch(Predicate<? super T> predicate)
boolean anyMatch(Predicate<? super T> predicate)
boolean noneMatch(Predicate<? super T> predicate)
```
```
boolean noFailed = stuStream.anyMatch(s->s.getTotalScore() <= 100);
```
```
Optional<Student> stu = stuStream.filter(s->s.getTotalScore() <= 10).findFirst();
```

### 통계 - count(), sum(), average(), max(), min()
- IntStream과 같은 기본형 스트림에는 스트림의 요소들에 대한 통계 정보를 얻을 수 있는 메서드들이 있다.
- 기본형 스트림이 아닌 경우에는 통계 관련 메서드가 3개만 있다(count(), max(), min())

### 리듀싱 - reduce()
- 스트림의 요소를 줄여나가면서 연산을 수행하고 최종결과를 반환한다.
- 매개변수의 타입은 BinaryOperator<T>이다.
- 처음 두 요소를 가지고 연산한 결과를 가지고 그 다음 요소를 연산한다.

```
Optional<T> reduce(BinaryOperator<T> accumulator)
T reduce(T identity, BinaryOperator<T> accumulator)
```

**참고** BinaryOperator<T>는 BiFunction의 하위 인터페이스이며 BiFunction<T,T,T>와 동등하다.
- 최종연산 count(), sum(), max(), min() 등은 내부적으로 모두 reduce()를 이용해서 작성된 것이다.

```
int count = intStream.reduce(0, (a, b) -> a + 1);
int sum = intStream.reduce(0, (a,b) -> a + b);
int max = intStream.reduce(Integer.MIN_VALUE, (a, b) -> a>b?a:b);
int min = intStream.reduce(Integer.MAX_VALUE, (a, b) -> a<b?a:b);
```

#### day19/StreamEx5.java
```java
package day19;
import java.util.*;
import java.util.stream.*;
public class StreamEx5 {
	public static void main(String[] args) {
		String[] strArr = {
			"Inheritance", "Java", "Lambda", "stream",
			"optionalDouble", "IntStream", "count", "sum"
		};
		Stream.of(strArr).forEach(System.out::println);
		
		boolean noEmptyStr = Stream.of(strArr).noneMatch(s->s.length() == 0);
		Optional<String> sWord = Stream.of(strArr)
					.filter(s->s.charAt(0) == 's').findFirst();
		
		System.out.println("noEmptyStr=" + noEmptyStr);
		System.out.println("sWord=" + sWord.get());
		
		// Stream<String[]>을 IntStream으로 변환
		IntStream intStream1 = Stream.of(strArr).mapToInt(String::length);
		IntStream intStream2 = Stream.of(strArr).mapToInt(String::length);
		IntStream intStream3 = Stream.of(strArr).mapToInt(String::length);
		IntStream intStream4 = Stream.of(strArr).mapToInt(String::length);
		
		int count = intStream1.reduce(0, (a,b) -> a + 1);
		int sum = intStream2.reduce(0,  (a,b) -> a + b);
		
		OptionalInt max = intStream3.reduce(Integer::max);
		OptionalInt min = intStream4.reduce(Integer::min);
		
		System.out.println("count=" + count);
		System.out.println("sum=" + sum);
		System.out.println("max=" + max.getAsInt());
		System.out.println("min=" + min.getAsInt());
	}
}
```
- 실행결과
```
Inheritance
Java
Lambda
stream
optionalDouble
IntStream
count
sum
noEmptyStr=true
sWord=stream
count=8
sum=58
max=14
min=3
```

## collect()
- 스트림의 최종연산, 매개변수로 컬렉터를 필요로 한다.
```
Object collect(Collector collector) // Collector를 구현한 클래스의 객체를 매개변수로
```
```
collect() 스트림의 최종연산, 매개변수로 컬렉터를 필요로 한다.
Collector 인터페이스, 컬렉터는 이 인터페이스를 구현해야 한다.
Collectors 클래스, static 메서드로 미리 작성된 컬렉터를 제공한다.
```
### 스트림 컬렉션과 배열로 변환 - toList(), toSet(), toMap(), toCollection(), toArray()
- 스트림의 모든 요소를 컬렉션에 수집하고자 할때는 Collectors클래스의 toList()와 같은 메서드를 사용한다.
- List나 Set이 아닌 특정 컬렉션을 지정하려면 toCollection()에 해당하는 컬렉션의 생성자 참조를 매개변수로 넣어준다.
```
List<String> names = stuStream.map(Student::getName).collect(Collectors.toList());
ArrayList<String> list = names.stream().collect(Collectors.toCollection(ArrayList::new));
```
- toMap()
```
Map<String, Person> map = personStream.collect(Collectors.toMap(p->p.getRegId(), p->p));
Map<String, Person> map = personStream.collect(Collectors.toMap(p->p.getRegId(), Function.identity()));
```
- toArray()
	- 매개변수로 해당타입의 생성자를 지정해야 한다. 
	- 매개변수를 지정하지 않으면 반환되는 배열의 타입은 'Object[]'이다.
```
Student[] stuNames = studentStream.toArray(Student[]::new);  // OK
Student[] stuNames = studentStream.toArray(); // 에러 발생
Object[] stuNames = studentStream.toArray(); // OK
```
### 통계 - counting(), summingInt(), averagingInt(), maxBy(), minBy()
```
long count = stuStream.count();
long count = stuStream.collect(Collectors.counting());
long totalScore = stuStream.mapToInt(Student::getTotalScore).sum();
long totalScore = stuStream.collect(Collectors.summingInt(Student::getTotalScore));
OptionalInt toScore = studentStream.mapToInt(Student::getTotalScore).max();
Optional<Student> topStudent = stuStream.max(Comparator.comparingInt(Student::getTotalScore));
Optional<Student> topStudent = stuStream.collect(maxBy(Comparator.comparingInt(Student::getTotalScore)));
IntSummaryStatistics stat = stuStream.mapToInt(Student::getTotalScore).summaryStatistics();
IntSummaryStatistics stat = stuStream.collect(summarizingInt(Student::getTotalScore));
```
### 리듀싱 - reducing()
```
Collector reducing(BinaryOperator<T> op)
Collector reducing(T identity, BinaryOperator<T> op)
Collector reducing(U identity, Function<T, U> mapper, BinaryOperator<U> op)
```
```
IntStream intStream = new Random().ints(1, 46).distinct().limit(6);
OptionalInt max = intStream.reduce(Integer::max);
Optional<Integer> max = intStream.boxed().collect(Collectors.reducing(Integer::max));
long sum = intStream.reduce(0, (a, b) -> a + b);
long sum = intStream.boxed().collect(Collectors.reducing(0, Student::getTotalScore, Integer::sum)));
```
IntStream에는 매개변수 3개짜리 collect()만 정의되어 있으므로 매개변수 1개짜리 collect()를 쓰려면 boxed()를 통해 IntStream을 Stream<Integer>로 변환해야 한다.

