
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


