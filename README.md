### [📃Google Java Style Guide 원문📃](https://google.github.io/styleguide/javaguide.html#s3.4.1-one-top-level-class)

# 1. 소개

이 문서는 Java ™ 프로그래밍 언어의 소스 코드에 대한 Google 코딩 표준의 완전한 정의로 사용됩니다. Java 소스 파일은 여기에있는 규칙을 준수하는 경우에만 Google 스타일 로 설명됩니다 .

다른 프로그래밍 스타일 가이드와 마찬가지로 다루는 문제는 형식화의 미적 문제뿐 아니라 다른 유형의 규칙이나 코딩 표준에도 적용됩니다. 그러나이 문서는 주로 우리가 보편적으로 따르는 엄격하고 빠른 규칙 에 초점을 맞추고 명확하게 시행 할 수없는 조언 (인간 또는 도구)을 제공 하지 않습니다.

## 1.1 용어 참고

이 문서에서 달리 명시되지 않는 한 :

용어 `class`는 "일반적인"class, enum class, interfacec 또는 어노테이션 유형 ( @interface) 을 의미하기 위해 포괄적으로 사용됩니다.
`(클래스의) member` 라는 용어 는 중첩 된 클래스, 필드, 메서드 또는 생성자 를 의미하기 위해 포괄적으로 사용됩니다 .
즉, 이니셜 라이저와 주석을 제외한 클래스의 모든 최상위 콘텐츠입니다.
`comment` 이라는 용어 는 항상 구현 주석을 의미합니다 . 우리는 "documentation comments"이라는 문구를 사용하지 않고 "Javadoc"이라는 일반적인 용어를 사용합니다.
문서 전체에 "용어 노트"가 가끔 나타납니다.

## 1.2 가이드 노트

이 문서의 예제 코드는 표준 이 아닙니다 . 즉, 예제는 Google 스타일이지만 코드를 표현하는 유일한 세련된 방법을 설명하지 못할 수 있습니다 . 예제에서 선택한 선택적 형식 지정은 규칙으로 강제되지 않아야합니다.

# 2 소스 파일 기본 사항

## 2.1 파일 이름

소스 파일 이름은 포함 된 최상위 클래스의 대소 문자 구분 이름과 `.java`확장자로 구성됩니다.

## 2.2 파일 인코딩 : UTF-8

소스 파일은 UTF-8 로 인코딩됩니다 .

## 2.3 특수 문자

### 2.3.1 공백 문자

줄 종결 자 시퀀스를 제외하고 ASCII horizontal space character (0x20)는 소스 파일의 아무 곳에나 나타나는 유일한 공백 문자입니다. 이것은 다음을 의미합니다.

1. 문자열 및 문자 리터럴의 다른 모든 공백 문자는 이스케이프됩니다.
2. 탭 문자는 들여 쓰기에 사용 되지 않습니다 .

### 2.3.2 특수 이스케이프 시퀀스

특수 이스케이프 문자들( \b, \t, \n, \f, \r, ", '과 \)은 해당 진수(\012) 또는 유니 코드 (\u000a) 이스케이프 대신 해당 문자가 사용된다.

### 2.3.3 Non-ASCII 문자

Non-ASCII 문자의 경우 실제 유니 코드 문자 (예 : ∞)또는 동등한 유니 코드 이스케이프 (예 : \u221e) 가 사용됩니다. 유니 코드가 문자열 리터럴 및 주석 외부에서 이스케이프하는 것은 권장되지 않지만 코드를 더 쉽게 읽고 이해할 수 있는 방법에 따라 사용할 수도 있다.

💡 Tip : 유니 코드 이스케이프 케이스 및 실제 유니 코드 문자가 사용되는 경우에도 설명하는 주석이 매우 유용 할 수 있습니다.

#### Examples

| Examples                                               | Discussion                                                   |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| String unitAbbrev = "μs";                              | 최고 : 댓글이 없어도 완벽하게 선명합니다.                    |
| String unitAbbrev = "\u03bcs"; // "μs"                 | 허용되지만이 작업을 수행 할 이유가 없습니다.                 |
| String unitAbbrev = "\u03bcs"; // Greek letter mu, "s" | 허용되지만 어색하고 실수하기 쉽습니다.                       |
| String unitAbbrev = "\u03bcs";                         | 나쁨 : 독자는 이것이 무엇인지 전혀 모릅니다.                 |
| return '\ufeff' + content; // byte order mark          | 좋음 : 인쇄 할 수없는 문자에는 이스케이프를 사용하고 필요한 경우 주석을 추가합니다. |

💡 Tip : 일부 프로그램이 Non-ASCII 문자를 제대로 처리하지 못할 수 있다는 두려움 때문에 코드의 가독성을 낮추지 마십시오. 이런 일이 발생하면 해당 프로그램이 중단 되고 수정 해야합니다 .

# 3 소스 파일 구조

소스 파일은 다음 순서 로 구성됩니다 .

1. 라이센스 또는 저작권 정보 (있는 경우에)
2. Package 구문
3. Import 구문
4. 정확히 하나의 최상위 Class

❗️정확히 하나의 빈 줄이 각 섹션을 구분합니다❗️

## 3.1 라이선스 또는 저작권 정보 (있는 경우)

라이센스 또는 저작권 정보가 파일에 속하면 여기에 속합니다.

## 3.2 Package 구문

패키지 문은 줄 바꿈되지 않습니다 .
열 제한 (섹션 4.4참고 , 열 제한 : 100 )은 패키지 문에 적용되지 않습니다.

## 3.3 Import 구문

### 3.3.1 와일드 카드 가져 오기 없음

static 또는 기타 와일드 카드 `import` 는 사용하지 않습니다 .

### 3.3.2 줄 바꿈 없음

Import 문은 줄 바꿈되지 않습니다 .
열 제한 (섹션 4.4 참고, 열 제한 : 100 )은 import 문에 적용되지 않습니다.

### 3.3.3 순서 및 간격

`imports`는 다음과 같은 순서로 쓴다.

1. 단일 블록에서 모든 static imports.
2. 단일 블록의 모든 non-static imports.

static imports와 non-static imports가 모두있는 경우 하나의 빈 줄이 두 블록을 구분합니다.
❗️import 문 사이에는 다른 빈 줄이 없습니다❗️

각 블록 내에서 가져온 이름은 ASCII 정렬 순서로 나타납니다.
( 참고 : 여기서 '.'가 ';'앞에 정렬되므로 ASCII 정렬 순서 인 import 문과 동일하지 않습니다 .)

### 3.3.4 클래스에는 static import를 하지 않는다.

static 중첩 클래스에는 static import가 사용되지 않습니다.
그들은 일반적인 import를 사용합니다.

## 3.4 클래스 선언

### 3.4.1 정확히 하나의 최상위 클래스 선언

소스 파일마다 각자의 최상위 클래스가 존재한다.

### 3.4.2 클래스 내용 순서

클래스의 멤버 및 이니셜 라이저에 대해 선택한 순서는 이해하는데 큰 영향을 미칠 수 있습니다.
그러나 이를 수행하는 방법에 대한 정해진 방법은 없습니다.
다른 클래스는 다른 방식으로 내용 순서를 정할 수 있습니다.

중요한 것은 각 클래스가 몇 가지 논리적 순서를 사용한다는 것입니다.
이 순서는 관리자가 요청하면 설명 할 수 있어야 한다.
예를 들어, 새로운 메서드가 클래스 끝에 습관적으로 추가되었다면 논리적 순서가 아닌 "추가 된 날짜 별 시간순"순서이다.

#### 3.4.2.1 Overloads (오버로드) : 🚫 Never 위치 분할 🚫

클래스에 여러 생성자 또는 동일한 이름을 가진 여러 메서드가있는 경우 이들은 사이에 다른 코드 없이 (개인 멤버도 포함되지 않음) 순차적으로 나타나야 한다.

# 4 Formatting

##### 용어 참고

`block-like construct (블록과 같은 구조)` 는 클래스, 메서드 또는 생성자의 본문을 나타냅니다. 배열 이니셜 라이저 에 대한 섹션 4.8.3.1에 따라 모든 배열 초기화 블록은 는 선택적으로 블록과 유사한 구조 인 것처럼 처리 될 수 있습니다.

## 4.1 괄호

### 4.1.1 선택 사항인 경우에서도 중괄호가 사용됩니다.

`if, else, for, do 및 while문` 또는 body가 비어 있거나 단 하나의 문이 포함 된 경우에도 괄호가 쓰인다.

### 4.1.2 비어 있지 않은 블록 : K & R 스타일

괄호는 비어 있지 않은 블록 및 블록 유사 구조에 대해 Kernighan 및 Ritchie 스타일 ("Egyptian brackets (이집트 대괄호)")을 따릅니다 .

- 여는 중괄호 앞에 줄 바꿈이 없습니다.
- 여는 중괄호 뒤의 줄 바꿈.
- 닫는 중괄호 앞의 줄 바꿈.
- 닫는 중괄호 뒤의 줄 바꿈 ( 중괄호가 명령문을 종료하거나 메서드, 생성자 또는 명명 된 클래스 의 본문을 종료하는 경우)
- 중괄호 뒤에 `else` 또는 쉼표`,` 가 오면 줄 바꿈 이 없습니다.

#### Examples

```
return () -> {
  while (condition()) {
    method();
  }
};

return new MyClass() {
  @Override public void method() {
    if (condition()) {
      try {
        something();
      } catch (ProblemException e) {
        recover();
      }
    } else if (otherCondition()) {
      somethingElse();
    } else {
      lastThing();
    }
  }
};
```

Enum 클래스에 대한 몇 가지 예외는 섹션 4.8.1, Enum 클래스에 있습니다.

### 4.1.3 빈 블록 : 간결 할 수 있음

빈 블록 또는 블록과 유사한 구조는 K & R 스타일 일 수 있습니다 ( 섹션 4.1.2에 설명 됨 ).
또는 다중 블록 명령문 (다중 블록을 직접 포함하는 명령문 : `if/else`또는 `try/catch/finally`)의 일부가 아닌 경우 ({}) 사이에 문자나 줄 바꿈없이 열린 직후 닫을 수 있습니다 .

#### Examples

```
  // 허용
  void doNothing() {}

  // 허용
  void doNothingElse() {
  }
  // 허용되지 않음 : 멀티 블럭 구문에서는 간결한 빈 블럭을 사용할 수 없다.
  try {
    doSomething();
  } catch (Exception e) {}
```

## 4.2 블록 들여 쓰기 : +2 공백

새 블록 또는 블록과 유사한 구조가 열릴 때마다 들여 쓰기가 두 칸씩 증가합니다.
블록이 끝나면 들여 쓰기는 이전 들여 쓰기 수준으로 돌아갑니다. 들여 쓰기 수준은 블록 전체의 코드와 주석 모두에 적용됩니다. (섹션 4.1.2, 비어 있지 않은 블록 : K & R 스타일 의 예를 참조하십시오 .)
**🪐근데 우테코에서는 2칸이 아닌 4칸 들여쓰기를 사용하라 했음!🪐**

## 4.3 한 줄에 하나의 문

각 문 뒤에는 줄 바꿈이 있습니다.

## 4.4 열 제한 : 100

Java 코드의 열 제한은 100 자입니다.
"character"는 모든 유니 코드 코드 포인트를 의미합니다.
아래 언급 된 경우를 제외하고이 제한을 초과하는 모든 줄은 섹션 4.5, 줄 바꿈에 설명 된대로 줄 바꿈해야합니다 .

각 유니 코드 코드 포인트는 표시 너비 크기에 상관없이 하나의 문자로 계산됩니다.
예를 들어 fullwidth characters(일본어, 한자, 한글, 숫자)를 사용 하는 경우이 규칙보다 먼저 줄을 줄 바꿈하도록 선택할 수 있습니다.

#### 예외

1. 열 제한을 따를 수없는 행 (예 : Javadoc의 긴 URL 또는 긴 JSNI 메소드 참조).
2. `package`및 `import`문 (섹션 3.2 패키지 문 및 3.3 Import 문 참조 ).
3. 셸에 복붙되는 주석의 명령 줄

## 4.5 줄 바꿈

##### 용어 참고

코드를 하나의 줄에서 여러 줄로 나눌 때이 작업을 줄 바꿈 이라고 합니다 .

모든 상황에서 줄 바꿈하는 방법을 정확히 보여주는 공식은 없습니다.
동일한 코드를 줄 바꿈하는 여러 가지 유효한 방법이 많이 있습니다.

참고 : 줄 바꿈의 일반적인 이유는 열 제한을 초과하지 않도록하는 것이지만 실제로 열 제한에 맞는 코드도 작성자의 재량에 따라 줄 바꿈 될 수 있습니다.

💡 Tip : 메서드 또는 지역 변수를 추출하면 줄 바꿈없이 문제를 해결할 수 있습니다.

### 4.5.1 어디서 줄바꿈 하는가?

줄 바꿈의 주요 지침은 더 높은 문법 수준 에서 중단하는 것 입니다.

또한:

1. 비 할당 연산자 에서 줄이 끊어 지면 기호 앞에 끊어 집니다.
   (이것은 C ++ 및 JavaScript와 같은 다른 언어의 Google 스타일에서 사용되는 것과 다릅니다.)
   이는 다음 "operator-like"기호에도 적용됩니다.

- 점 구분 기호 ( .)
- 메서드 참조의 두 콜론 ( ::)
- Type 바운드의 앰퍼샌드 (<T extends Foo & Bar>)
- catch 블록의 파이프 (catch (FooException | BarException e))

1. 할당 연산자 에서 줄이 끊어지면 일반적으로 기호 뒤에 끊어 지지만 어느 쪽이든 허용됩니다.

- 이는 확장 for(foreach) 문 에서 "assignment-operator-like" 콜론에도 적용됩니다 .

1. 메서드 또는 생성자 이름은 그 뒤에 오는 여는 괄호가 있을 때 ( `()`까지 쓰고 줄바꿈)
2. 쉼표 ( ,)는 그 앞에있는 토큰에 연결되어 있을 때
3. lambda의 본문이 중괄호가없는 단일 식으로 구성된 경우 화살표 바로 뒤에 줄 바꿈이있을 수 있다.
   이를 제외하고는 lambda의 화살표 옆에서 줄이 끊어지지 않습니다.Examples

#### Examples

```
MyLambda<String, Long, Object> lambda =
    (String label, Long value, Object obj) -> {
        ...
    };

Predicate<String> predicate = str ->
    longExpressionInvolving(str);
```

참고 : 줄 바꿈의 기본 목표 는 최소한의 줄에 맞는 코드가 아니라 명확한 코드를 만드는 것입니다.

### 4.5.2 연속 줄을 최소 +4 공백 들여 쓰기

줄 바꿈시 첫 번째 줄 (각 연속 줄 ) 뒤의 각 줄 은 원래 줄에서 적어도 +4만큼 들여 쓰기됩니다.

연속 줄이 여러 개인 경우 원하는대로 들여 쓰기를 +4 이상으로 변경할 수 있습니다.
일반적으로 두 개의 연속 줄은 구문 상 병렬 요소로 시작하는 경우에만 동일한 들여 쓰기 수준을 사용합니다.

수평 정렬 에 관한 섹션 4.6.3은 특정 토큰을 이전 행과 정렬하기 위해 가변 수의 공백을 사용하는 권장되지 않는 관행을 다룹니다.

## 4.6 공백

### 4.6.1 세로 공백

하나의 빈 줄은 이럴 때 나타난다:

1. 연속적인 멤버 또는 클래스의 초기화 : 필드, 생성자, 메소드, 중첩 클래스, 정적 초기화 그리고 인스턴스 초기화

- 예외 : 두 개의 연속 된 필드 사이에 다른 코드가없는 빈 줄은 선택 사항입니다. 이러한 빈 줄은 필요에 따라 필드의 논리적 그룹 을 만드는 데 사용됩니다 .
- 예외 : enum 상수 사이의 빈 줄은 섹션 4.8.1 에서 다룹니다 .

1. 이 문서의 다른 섹션에서 요구하는대로 (예 : 섹션 3, 소스 파일 구조 및 섹션 3.3, import 문 ).
   예를 들어 코드를 논리적 하위 섹션으로 구성하는 명령문 사이와 같이 가독성을 향상시키는 모든 곳에 빈 줄 하나가 나타날 수 있습니다.
   첫 번째 멤버나 이니셜 라이저 앞이나 클래스의 마지막 멤버 나 이니셜 라이저 뒤의 빈 줄은 권장되거나 권장되지 않습니다.

여러 개의 연속 된 빈 줄이 허용되지만 필수 (또는 권장)는 아닙니다.

### 4.6.2 수평 공백

언어 또는 기타 스타일 규칙에서 요구하는 경우 외에 리터럴, 주석 및 Javadoc을 제외하고 단일 ASCII 공간 (띄어쓰기)은 다음 위치 에만 나타납니다 .

1. 예약어를 나누는 경우 : 해당 줄에서 뒤에 오는 여는 괄호 `(`에서 `if, for`또는 `catch` 이후 나오는 여는 괄호에서 사용
2. 예약어를 나누는 경우 : `else`또는 `catch` 이후 나오는 닫는 중괄호`}`에서 분리
3. 여는 중괄호 `{` 앞 , 두 가지 예외 :

- @SomeAnnotation({a, b}) (공백이 사용되지 않음)
- String[][] x = {{"foo"}};( {{아래 8 번 항목 사이에 공백이 필요하지 않음 )

1. 이항 또는 삼항 연산자의 양쪽 : 이는 다음 "operator-like"기호에도 적용됩니다.

- 인접한 Type 바인딩의 앰퍼샌드 : <T extends Foo & Bar>
- 여러 예외를 처리하는 catch 블록에 대한 파이프 : catch (FooException | BarException e)
- for("foreach") 문 에서 콜론 `:`
- 람다 식의 화살표 : (String str) -> str.length()
- 하지만 아래 같은 경우에서는 사용하지 않는다.
  - 메소드 참조 의 두 콜론 `::`은 다음과 같이 작성됩니다 : Object::toString
  - 다음`.`과 같이 쓰여진 점 구분 기호 : object.toString()

1. 캐스트 뒤 ,`:;`또는 닫는 괄호 `)`
2. `//`줄 끝 주석을 시작하는 이중 슬래시의 양쪽 . 여기에서는 여러 개의 공백이 허용되지만 필수는 아닙니다.
3. 선언의 type과 변수 사이 : List list
4. (선택 사항) 배열 선언문 괄호 안에 공백 :new int[] {5, 6} 또는 new int[] { 5, 6 }
5. type annotation과 [] 또는 ...

이 규칙은 줄의 시작 또는 끝에 추가 공백을 요구하거나 금지하는 것으로 해석되지 않고 내부 공간 만을 다룬다 .

### 4.6.3 수평 정렬 : 필요 없음

#### 용어 참고

수평 정렬은 특정 토큰이 이전 줄의 다른 특정 토큰 바로 아래에 표시되도록 코드에 다양한 수의 추가 공백을 추가하는 방법입니다.

이 관행은 허용되지만 Google 스타일에서 요구 하는 것은 아닙니다 .
이미 사용 된 장소에서 수평 정렬 을 유지할 필요조차 없습니다 .

다음은 정렬없이 정렬을 사용하는 예입니다.

```
private int x; // OK
private Color color; // OK

private int   x;      // OK, but future edits
private Color color;  // 맞춰지지 않은 상태로 둘 수 있음
```

💡 Tip : 정렬은 가독성에 도움이 될 수 있지만 향후 유지 관리에 문제가됩니다.
한 줄만 수정하면되는 미래를 생각해보십시오. 이 변경으로 이전에 만족 스러웠던 서식이 엉망이 될 수 있습니다. 더 자주 개발자에게 근처 줄의 공백을 조정하라는 메시지를 표시하여 계단식 일련의 재 포맷을 트리거 할 수 있습니다. 그 한 줄 변경은 이제 "폭발 반경"을 갖습니다. 이것은 최악의 경우 무의미한 작업을 초래할 수 있지만 기껏해야 버전 기록 정보를 손상시키고 검토 자의 속도를 늦추고 병합 충돌을 악화시킵니다.

## 4.7 그룹화 괄호 : 권장

선택적 그룹화 괄호는 작성자와 검토자가 코드가 없으면 코드가 잘못 해석 될 가능성이 없으며 코드를 읽기 쉽게 만들지 않았다는 데 동의하는 경우에만 생략됩니다. 모든 독자가 자바 연산자 우선 순위 테이블이 있다고 가정하는 것은 옳지 않다. 우선순위가 명확해도 괄호로 감싸라❗️

## 4.8 특정 구조

### 4.8.1 Enum 클래스

enum 상수 뒤에 오는 각 쉼표 뒤에 줄 바꿈은 선택 사항입니다.
추가 빈 줄 (일반적으로 하나만)도 허용됩니다.

#### Example

```
  private enum Answer {
  YES {
    @Override public String toString() {
      return "yes";
    }
  },

  NO,
  MAYBE
}
```

method와 주석이 없는 enum class는 배열 초기화와 같은 포맷으로 적의될 수 있다.

```
private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }
```

enum 클래스 는 classes 이므로 클래스 형식 지정에 대한 다른 모든 규칙이 적용됩니다.

### 4.8.2 변수 선언

#### 4.8.2.1 선언 당 하나의 변수

모든 변수 선언 (필드 또는 로컬)은 하나의 변수 만 선언합니다.
이러한 선언 `int a, b;`은 사용되지 않습니다.

예외 :for 루프 헤더에 여러 변수 선언이 허용됩니다 .

#### 4.8.2.2 필요할 때 선언

지역 변수는 포함 블록이나 블록과 유사한 구조의 시작 부분에서 습관적으로 선언 되지 않습니다 .
대신 지역 변수는 범위를 최소화하기 위해 처음 사용되는 지점(이유가 있는)에 가깝게 선언됩니다.
지역 변수 선언에는 일반적으로 이니셜 라이저가 있거나 선언 직후에 초기화됩니다.

### 4.8.3 Array

#### 4.8.3.1 배열 이니셜 라이저 : "block-like"

모든 배열 이니셜 라이저는 선택적 으로 "block-like construct"인 것처럼 형식화 될 수 있습니다.
다음의 경우 모두 가능하다:

```
  new int[] {           new int[] {
  0, 1, 2, 3            0,
}                       1,
                        2,
new int[] {             3,
  0, 1,               }
  2, 3
}                     new int[]
                          {0, 1, 2, 3}
```

#### 4.8.3.2 C 스타일 배열 선언 없음

대괄호 는 변수가 아닌 type의 일부를 형성 합니다 : ⭕️ String[] args ❌ String args[]

### 4.8.4 Switch 문

#### 용어 참고

스위치 블록 의 중괄호 안에는 하나 이상의 구문 그룹이 있습니다.
각 구문 그룹은 하나 이상의 switch 라벨 (either `case FOO:` or `default:`)과 하나 이상의 명령문 (또는 마지막 명령문 그룹의 경우 0 개 이상의 명령문)으로 구성됩니다.

#### 4.8.4.1 들여 쓰기

다른 블록과 마찬가지로 스위치 블록의 내용은 +2로 들여 쓰기됩니다.

스위치 레이블 뒤에는 줄 바꿈이 있고 들여 쓰기 수준은 마치 블록이 열려있는 것처럼 +2가 증가합니다. 다음 스위치 레이블은 마치 블록이 닫힌 것처럼 이전 들여 쓰기 수준으로 돌아갑니다.

#### 4.8.4.2 Fall-through : 주석

Switch 블록 내에서 각 문 그룹 중 하나 (break, continue, return또는 발생한 예외)가 돌연 중료되서나, 다음 구문으로 넘어가게 적을 수 있다. 여기에는 주석을 달 수 있다. (일반적으로 // fall through).
이 특수 주석은 스위치 블록의 마지막 명령문 그룹에는 필요하지 않습니다. 예:

```
  switch (input) {
  case 1:
  case 2:
    prepareOneOrTwo();
    // fall through
  case 3:
    handleOneTwoOrThree();
    break;
  default:
    handleLargeNumber(input);
}
```

`case 1:`다음에 주석이 필요하지 않으며 명령문 그룹의 끝에서만 주석이 필요하다.

#### 4.8.4.3 default 케이스 존재

각 switch 문에는 default 코드가없는 경우에도 default문 그룹이 포함됩니다.

예외 : enum 유형에 대한 switch 문은 해당 유형의 가능한 모든 경우를 포함하는 명시적 케이스를 처리한 경우 명령문 그룹을 생략 할 수 있습니다 .
이를 통해 IDE 또는 기타 정적 분석 도구는 누락 된 사례가있는 경우 경고를 발행 할 수 있습니다.

### 4.8.5 Annotations

클래스, 메서드 또는 생성자에 적용되는 Annotations은 documentation block 바로 뒤에 나타나며 각 어노테이션은 자체 줄에 나열됩니다 (즉, 한 줄에 하나의 어노테이션). 이러한 줄 바꿈은 줄 바꿈을 구성하지 않으므로 (섹션 4.5, 줄 바꿈 ) 들여 쓰기 수준이 증가하지 않습니다.

#### Example

```
@Override
@Nullable
public String getNameIfPresent() { ... }
```

예외 :파라미터가 없는 단일 anotation은 한 줄 맨 처음에 쓸 수 있다 :

#### Example

```
@Override public int hashCode() { ... }
```

필드에 적용되는 Annotations도 documentation block 바로 뒤에 나타나지만 이 경우 여러 주석 (매개 변수화 가능)이 같은 줄에 나열 될 수 있습니다.

#### Example

```
@Partial @Mock DataLoader loader;
```

파라미터, 지역 변수 또는 타입에 대한 주석 형식화에 대한 특정 규칙은 없습니다.

### 4.8.6 주석

이 섹션에서는 구현 주석을 다룹니다 . Javadoc은 섹션 7, Javadoc 에서 별도로 다루고 있습니다.

줄 바꿈 앞에는 임의의 공백과 구현 주석이 올 수 있습니다.
이러한 주석은 행을 공백이 아닌 것으로 렌더링합니다.

#### 4.8.6.1 블록 주석 스타일

블록 주석은 주변 코드와 동일한 수준에서 들여 쓰기됩니다. `/* ... */`스타일이나 `// ...`스타일이 있을 수 있습니다 . 여러 줄 `/* ... */`주석의 경우 후속 줄은 이전 줄에 `*`정렬 된 것으로 시작해야합니다.

```
/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
```

주석은 별표 또는 기타 문자로 그려진 박스에 포함되지 않습니다.

💡 Tip : 여러 줄 주석을 작성할 `/* ... */`때 필요한 경우 자동 코드 포맷터가 줄을 다시 줄 이도록하려면 (단락 스타일) 스타일을 사용하십시오. 대부분의 포맷터는 `// ...`스타일 주석 블록 에서 줄을 다시 감싸지 않습니다 .

### 4.8.7 Modifiers (접근 제한자)

클래스 및 멤버 Modifiers는 있는 경우 Java 언어 사양에서 권장하는 순서로 나타납니다.

```
public protected private abstract default static final transient volatile synchronized native strictfp
```

### 4.8.8 숫자 리터럴

long값을 갖는 정수 리터럴 L은 소문자가 아닌 대문자 접미사를 사용합니다 (digit(1)와의 혼동을 피하기 위해 ).
예를 들어, ⭕️ 3000000000L ❌ 3000000000l.

# 5 Naming

## 5.1 모든 식별자에 공통적인 규칙

식별자는 ASCII 문자와 숫자만 사용하며 `_`를 사용하기도 하여서 표시됩니다.
따라서 각 유효한 식별자 이름은  \w+ 정규식과 일치합니다.

Google 스타일에서는 특수 접두사 또는 접미사가 사용 되지 않습니다 .
예를 들어,이 이름들은 구글 스타일이 아닙니다 : name_, mName, s_name와 kName.

## 5.2 식별자 유형별 규칙

### 5.2.1 Package 이름

패키지 이름은 모두 소문자이며 연속 된 단어는 단순히 함께 연결됩니다 (밑줄 없음).
예를 들어, ⭕️ com.example.deepspacenot ❌ com.example.deepSpace또는 com.example.deep_space.

### 5.2.2 클래스 이름

클래스 이름은 UpperCamelCase 로 작성됩니다.

클래스 이름은 일반적으로 명사 또는 명사구입니다.
예를 들어, Character 또는 ImmutableList.
Interface 이름은 명사 또는 명사 구 (예 : List) 일 수도 있지만 때로는 대신 형용사 또는 형용사 구 (예 : Readable) 일 수도 있습니다.

어노테이션 유형 이름 지정에 대한 특정 규칙이나 잘 확립 된 규칙은 없습니다.

테스트 클래스의 이름은 테스트중인 클래스의 이름으로 시작하고 `Test`를 끝에 붙여줍니다.
예를 들어, HashTest또는 HashIntegrationTest.

### 5.2.3 메서드 이름

메소드 이름은 lowerCamelCase 로 작성됩니다 .

메서드 이름은 일반적으로 동사 또는 동사 구입니다. 예를 들어, sendMessage또는 stop.

JUnit 테스트 메서드 이름에 밑줄이 표시되어 이름의 논리적 구성 요소를 구분할 수 있으며 각 구성 요소는 lowerCamelCase로 작성됩니다 .
한 가지 전형적인 패턴은 예를 들면 다음과 같습니다 .

```
<methodUnderTest>_<state>pop_emptyStack
```

테스트 방법의 이름을 정하는 올바른 방법은 없습니다.

### 5.2.4 Constant 이름

상수 이름은 `CONSTANT_CASE`을 사용한다: 모두 대문자로 밑줄`_`로 각 단어를 구분한다.
**🤔 constant ?**
constant는 내용이 완전히 불변하고 메서드에 감지 가능한 부작용이없는 정적 최종 필드입니다. 여기에는 primitives, Strings, immutable types, immutable collections of immutable types이 포함됩니다.
인스턴스의 상태가 변경 될 수있는 경우 상수가 아닙니다. 단순히 객체 변형을 막는 것이 목적이 아니다.

#### Example

```
// Constants
static final int NUMBER = 5;
static final ImmutableList<String> NAMES = ImmutableList.of("Ed", "Ann");
static final ImmutableMap<String, Integer> AGES = ImmutableMap.of("Ed", 35, "Ann", 32);
static final Joiner COMMA_JOINER = Joiner.on(','); // because Joiner is immutable
static final SomeMutableType[] EMPTY_ARRAY = {};
enum SomeEnum { ENUM_CONSTANT }

// Not constants
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set<String> mutableCollection = new HashSet<String>();
static final ImmutableSet<SomeMutableType> mutableElements = ImmutableSet.of(mutable);
static final ImmutableMap<String, SomeMutableType> mutableValues =
    ImmutableMap.of("Ed", mutableInstance, "Ann", mutableInstance2);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
```

이러한 이름은 일반적으로 명사 또는 명사 구입니다.

### 5.2.5 상수가 아닌 필드 이름

상수가 아닌 필드 이름 (정적 또는 기타)은 lowerCamelCase 로 작성됩니다 .

이러한 이름은 일반적으로 명사 또는 명사 구입니다.
예를 들어, computedValues또는 index.

### 5.2.6 파라미터 이름

파라미터 이름은 lowerCamelCase 로 작성됩니다 .

공용 메소드에서 한 문자 파라미터 이름은 피해야합니다.

### 5.2.7 지역 변수 이름

지역 변수 이름은 lowerCamelCase 로 작성됩니다 .

final, 불변인 경우에도 지역 변수는 상수로 간주되지 않으며 상수로 스타일을 지정해서는 안됩니다.

### 5.2.8 Type 변수 이름

각 유형 변수는 다음 두 가지 스타일 중 하나로 이름이 지정됩니다.

- 단일 대문자, 혹은 단일 숫자가 따라올 수 있다. (예 : E, T, X, T2)
- 클래스에 사용되는 형식의 이름 (섹션 5.2.2, 클래스 이름 참조 ) 뒤에 대문자 T(예 : RequestT, FooBarT).

## 5.3 카멜 케이스 : 정의 된 단어들에 대하여

두문자어 또는 "IPv6"또는 "iOS"와 같은 비정상적인 구조가있는 경우와 같이 영어 구를 낙타 대문자로 변환하는 합리적인 방법이 여러 가지 있습니다. 예측 가능성을 높이기 위해 Google 스타일은 다음과 같은 (거의) 결정론적 체계를 지정합니다.

#### 산문 형식 이름으로 시작 :

1. 구를 일반 ASCII로 변환하고 어퍼스토로피를 제거하십시오. 예를 들어 "Müller's algorithm"은 "Muellers algorithm"이 될 수 있습니다.
2. 이 결과를 단어로 나누고 공백과 나머지 구두점 (일반적으로 하이픈)으로 분리합니다.

- 권장 : 일반적으로 사용되는 일반적인 camel-case 방식이 이미있는 단어가 있으면 이를 구성 부분으로 분할합니다 (예 : "AdWords"가 "ad words"가 됨). "iOS"와 같은 단어는 실제로 camel case 문자 자체 가 아닙니다 . 어떤 규칙도 위반하므로이 권장 사항은 적용되지 않습니다.

1. 이제 모든 것을 lowercase(약어 포함)하고 다음의 첫 번째 문자만 대문자로 표시합니다.

- 각 단어를 upper camel case로 표시하거나
- 첫 번째 단어를 제외한 각 단어는 lower camel case를 산출합니다.

1. 마지막으로 모든 단어를 단일 식별자로 결합합니다.

원래 단어의 대소 문자는 거의 완전히 무시됩니다.

#### Example

| Prose form                        | Correct                               | Incorrect         |
| --------------------------------- | ------------------------------------- | ----------------- |
| "XML HTTP request"                | XmlHttpRequest                        | XMLHTTPRequest    |
| "new customer ID"                 | newCustomerId                         | newCustomerID     |
| "inner stopwat                    | innerStopwatch                        | innerStopWatch    |
| "supports IPv6 on iOS?"           | supportsIpv6OnIos                     | supportsIPv6OnIOS |
| "YouTube importer"                | YouTubeImporter , YoutubeImporter , * |                   |
| * 허용되지만 권장되지는 않습니다. |                                       |                   |

참고 : 일부 단어는 영어에서 모호하게 하이픈으로 연결됩니다. 예를 들어 "nonempty"및 "non-empty"는 모두 정확하므로 메서드 이름 checkNonempty과 checkNonEmpty마찬가지로 모두 정확합니다.

# 6 프로그래밍 실습

## 6.1 @Override: 항상 사용

@Override가 허락 될 때마다 주석 으로 표시됩니다 .
여기에는 수퍼 클래스 메소드를 재정의하는 클래스 메소드, 인터페이스 메소드를 구현하는 클래스 메소드, 수퍼 인터페이스 메소드를 재 지정하는 인터페이스 메소드가 포함됩니다.

예외 : 부모 메서드가 @Deprecated인 경우 @Override 생략 할 수 있습니다 .

## 6.2 Caught exceptions : 무시되지 않음

아래에 언급 된 경우를 제외하고 Caught exceptions에 대한 응답으로 아무것도하지 않는 것은 매우 드뭅니다.
(일반적인 응답은 로그에 기록하거나 "불가능"하다고 판단되면으로 다시 던지는 것 AssertionError입니다.)

catch 블록에서 아무 조치도 취하지 않는 것이 진정으로 적절할 때 이것이 정당화되는 이유는 주석에 설명되어 야 한다.

```
try {
  int i = Integer.parseInt(response);
  return handleNumericResponse(i);
} catch (NumberFormatException ok) {
  // it's not numeric; that's fine, just continue
}
return handleTextResponse(response);
```

예외 : 테스트에서 포착 된 예외는 `expected`이름 이거나 이것으로 시작하는 경우 주석없이 무시 될 수 있습니다. 다음은 테스트중인 코드가 있음을 보장하기위한 매우 일반적인 관용구이기 때문에 주석이 필요 없다.

```
try {
  emptyStack.pop();
  fail();
} catch (NoSuchElementException expected) {
}
```

## 6.3 Static members : 클래스를 사용하여 정규화

정적 클래스 멤버에 대한 참조가 정규화되어야하는 경우 해당 클래스 type의 참조 또는 식이 아닌 해당 클래스의 이름으로 정규화됩니다.

```
Foo aFoo = ...;
Foo.aStaticMethod(); // good
aFoo.aStaticMethod(); // bad
somethingThatYieldsAFoo().aStaticMethod(); // very bad
```

6.4 Finalizers : 사용되지 않음

`Object.finalize`을 재정의하는 것은 극히 드뭅니다 .
💡 Tip : 하지 마십시오. 꼭 필요한 경우 먼저 효과적인 Java 항목 7, "종료 자 방지"를 매우주의 깊게 읽고 이해 한 후 수행하지 마십시오.

# 7 Javadoc

## 7.1 Formatting

### 7.1.1 일반 형식

Javadoc 블록 의 기본 형식은 다음 예와 같습니다.

```
/** 
 * 여러 줄의 Javadoc 텍스트가 여기에 작성됩니다. 
 * 일반적으로 래핑됩니다 ... 
 */ 
public int method ( String p1 ) { ... }
```

... 또는 이 예제에서 :

```
/ ** 특히 짧은 Javadoc입니다. * /
```

기본 형식은 항상 허용됩니다. Javadoc 블록 (주석 마커 포함) 전체가 한 줄에 들어갈 수있는 경우 한 줄 형식이 대체 될 수 있습니다. 이는 `@return`와 같은 블록 태그가없는 경우에만 적용됩니다 .

### 7.1.2 문단

하나의 빈 줄, 즉 정렬 된 선행 별표 ( *) 만 포함 된 줄은 단락 사이와 블록 태그 그룹 (있는 경우) 앞에 나타납니다. 첫 번째를 제외한 각 단락 `<p>`은 첫 번째 단어 바로 앞에 있으며 뒤에 공백이 없습니다.

### 7.1.3 블록 태그

사용되는 표준 "블록 태그"중 어떤 순서대로 표시 @param, @return, @throws, @deprecated,이 네 가지 유형의 빈 설명과 함께 표시되지 않습니다. 블록 태그가 한 줄에 들어가지 않으면 연속 줄은 @ 위치에서 4번 들여쓰기합니다.

### 7.2 The summary fragment

각 Javadoc 블록은 간단한 요약 조각으로 시작됩니다 .
이 조각은 매우 중요합니다.
클래스 및 메서드 인덱스와 같은 특정 컨텍스트에 나타나는 텍스트의 유일한 부분입니다.

이것은 완전한 문장이 아니라 명사구 또는 동사 구인 단편입니다. 그것은 `A {@code Foo} is a...` 또는 `This method returns...`로 시작하지 않습니다. `Save the record.` 처럼 완전한 필수 문장을 형성 않습니다. 그러나 조각은 완전한 문장 인 것처럼 대문자로 표시되고 구두점으로 표시됩니다.

💡 Tip : 일반적인 실수는 간단한 Javadoc을 형식으로 작성하는 것 ❌ `/** @return the customer ID */`입니다. 이것은 올바르지 않으며로 변경해야합니다 ⭕️`/** Returns the customer ID. */`.

## 7.3 Javadoc이 사용되는 곳

최소한, javadoc는 모든 존재하는 public 클래스, public 또는 protected 멤버 마다 나타난다.
몇 개의 예외는 다음과 같다.

Section 7.3.4, Non-required Javadoc에 설명 된대로 추가 Javadoc 컨텐츠가있을 수도 있습니다 .

### 7.3.1 예외 : 자명한 방법

javadoc는 "단순하고 명백한"방법 (getFoo같은)에 대한 선택 사항입니다. 이 경우는 진짜 foo를 반환하기 때문에 javadoc이 선택적이다.

중요 : 일반적인 독자가 알아야 할 관련 정보를 생략하는 것을 정당화하기 위해이 예외를 인용하는 것은 적절하지 않습니다. 예를 들어, `getCanonicalName`라는 메서드의 경우 일반적인 독자가 "Canonical Name"이라는 용어가 무엇을 의미하는지 모를 수 있다면 문서를 생략하지 마십시오.

### 7.3.2 예외 : overrides

Javadoc은 수퍼 타입 메소드를 오버라이드 하는 메소드에 항상 존재하는 것은 아닙니다.

### 7.3.4 필수가 아닌 Javadoc

다른 클래스와 멤버는 필요하거나 원하는대로 Javadoc이 있습니다 .

구현 주석이 클래스 또는 멤버의 전체적인 목적이나 동작을 정의하는 데 사용될 때마다 해당 주석은 대신 Javadoc로 작성됩니다 (사용 /**).

필수가 아닌 Javadoc은 섹션 7.1.2, 7.1.3 및 7.2의 형식화 규칙을 따르도록 엄격하게 요구되지는 않지만 물론 권장됩니다.
