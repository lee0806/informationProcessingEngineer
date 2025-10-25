
### 기본 문법

**타입 & 변수**

기본형 : boolean, byte, short, int, long, float, double, char
참조형 : String, 배열, 클래스, 인터페이스 등

기본형은 값 저장 / 참조형은 객체의 주소 저장

```
int n = 5;
String s = "hi"; // String은 참조형
```

**연산자 & 증감**

산술 : + - * / %
증감 : ++x (전위 : 먼저 증가) / x++ (후위 : 나중에 증가)
비교 : = =, !=, <, <=, >, >=
논리 : &&(AND), ||(OR), !(NOT)

```
int v = 10;
int a = ++v; // v = 11, a = 11
int b = v++; // b = 11, v = 12
```

**제어문**

```
if(cond) { ... } else { ... }
for (int i = 0; i < n; i++) { ... }
while (cond) { ... }
```

### 메서드(함수)

**선언과 호출**

```
static int add(int a, int b) { return a + b; }
int r = add(2, 3);
```

**오버로딩 (OverLoading) - "이름은 같지만, 파라미터와 시그니처가 다름"**

- 컴파일 시 결정
- 리턴타입만 다른건 오버로딩이 아님

```
static int calc(int n) { ... }
static int calc(String s) { ... } // 오버로딩 파라미터 타입이 다름
```

- 문제 20번 : calc("5")는 문자열 버전이 호출되고, 내부에서 Integer.valueOf(str)로 int로 변환한 후 다른 재귀식을 수행

**가변 인자**

```
static int sum(int... xs) {
	int t = 0;
	for (int x: xs) {
		t+=x;
	}
	return t;
}
```

### 클래스, 객체, 접근 제어자

**선언**

```
class Persion {
	String name; // 인스턴스 필드
	static int cnt; // 클래스(정적) 필드
}
```

**접근 제어자**

- public (어디에서나)
- protected (같은 패키지 + 상속관계)
- default (패키지)
- private (클래스 내부)

**static, instance**

static : 클래스 공용 (인스턴스 없이 접근)

인스턴스 : 객체마다 개별

```

Person.cnt++; // 클래스 공용
new Person().name = "Kim"; // 인스턴스별

```

**상속, 오버라이딩, 생성자, 초기화 순서**

```
class Parent { ... }
class Child extends Parent { ... }
```

**오버라이딩 (Overriding)** 
"이름/시그니처가 동일, 부모 메서드를 자식이 재정의"

런타임 시에 결정, 참조 타입이 부모여도 실제 객체(자식)의 메서드가 호출됨

@Override 사용

**필드 숨김 (Field Hiding)**

필드는 오버라이딩되지 않음

- 동일한 이름의 필드를 자식이 선언하면 숨김, 참조 타입 기준으로 접근

**생성자 호출 & 초기화 순서**

부모 필드 -> 부모 생성자
자식 필드 -> 자식 생성자
생성자 내부에서 호출한 메서드는 오버라이딩 시 자식의 메서드가 실행됨

> 생성자에서 호출한 메서드가 오버라이딩되어 있으면 자식 메서드가 먼저 실행될 수 있음 -> 아직 자식 필드가 완전히 초기화되지 않은 시점일 수 있어 주의

### 오해하는 override 관계

static 메서드의 경우 클래스에 속한 메서드이며 객체 (인스턴스)에 속한 메서드가 아니다.


```
public int x (int i) { return i + 2; }
```

-> 일반 메서드의 형태 : 인스턴스에 종속되므로 실제 객체 타입 기준으로 실행된다.

```
Parent ref = new Child();
ref.x(2);
```

- ref의 타입은 Parent지만
- 실제 생성된 객체는 Child이기 때문에
- Child.x(int)가 실행된다.
- 이는 동적 바인딩

```
public static String id() { return "p"; }
```
-> 이건 클래스에 소속된 정적 메서드 : 인스턴스와는 무관하게 참조 변수의 타입으로 결정된다.

```
Parent ref = new Child();
ref.id();
```

- ref의 타입이 Parent이므로 Parent.id()가 선택된다.
- 실제 ref가 Child 객체를 가리키더라도 컴파일러는 Parent 기준으로 해석된다.
- static 메서드는 "오버라이딩"이 아니라 "hind" 관계이다.



**예외처리 (try-catch-finally)**

```
try {
	// 예외 가능 코드
} catch (SpecificException e) {
	// 구체적 예외 먼저
} catch (Exception e) {
	// 최상위는 마지막
} finally {
	// 예외 여부와 무관하게 항상 실행
}
```

**예외 계층과 catch 순서**

- Exception은 최상위 - 항상 마지막에
- 더 구체적인 예외 (ArithmeticException 같은 ...)를 위에

**finally는 무조건 실행**

- 리턴 / 예외가 발생해도 finally는 항상 실행 (System.exit() 같은 종료는 예외된다.)

**예외 종류**

**ArithmeticException** : 정수형에서 0으로 나눗셈, 오버플로우 유발 연산 등 산술 연산 오류

```
int x = 5 / 0; // ArithmeticException
```

**ArrayIndexOutOfBoundsException** : 배열에 대해 유효 범위를 벗어난 인덱스 접근 (음수, length 이상)

```
int[] a = {1, 2, 3};
int x = a[3]; // 길이가 3이면 최대 인덱스는 2이므로 오류 발생
```

**NumberFormatException** : 숫자로 해석 불가능한 문자열을 정수 / 실수로 변환 시도

```
Integer.parseInt("12a"); // NumberFormatException
```

**NullPointerException** : null 참조에 점(.) 찍을 때

```
String s = null; s.length(); 
// NullPointerException
```

**ClassCastException** : 잘못된 다운캐스팅

```
Object o = "hi";
Integer x = (Integer) 0; // ClassCastException
```






**Exception** : 최상위 예외 타입




### 배열, 재귀, 분할 정복

