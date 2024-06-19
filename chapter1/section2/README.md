# 인터페이스

- 타입스크립트의 핵심 원칙 중 하나는 타입 검사가 값의 형태에 초점을 맞추고 있다는 것이다. 이를 `덕 타이핑` 혹은 `구조적 서브타이핑`이라고 한다.
- 타입스크립트에서 인터페이스는 이런 타입들의 이름을 짓는 역할을 하고 코드 안의 계약을 정의하는 것뿐만 아니라 프로젝트 외부에서 사용하는 코드의 계약을 정의하는 강력한 방법이다.

## 선택적 프로퍼티(Optional Properties)

- 선택적 프로퍼티들은 객체 안의 몇 개의 프로퍼티만 채워 함수에 전달하는 `option bags`같은 패턴을 만들때 유용하다.
- 선택적 프로퍼티는 선언에서 프로퍼티 이름 끝에 `?`를 붙여 표시한다.
- 선택적 프로퍼티의 이점은 인터페이스에 속하지 않는 프로퍼티의 사용을 방지하면서 사용 가능한 속성을 기술하는것이다.

```typescript
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig): { color: string; area: number } {
  let newSquare = { color: "white", area: 100 };
  if (config.color) {
    newSquare.color = config.color;
  }
  if (config.width) {
    newSquare.area = config.width * config.width;
  }
  return newSquare;
}

let mySquare = createSquare({ color: "black" });
```

## 읽기전용 프로퍼티(Readonly Properties)

- 일부 프로퍼티들은 객체가 처음 생성될때만 수정 가능해야 한다.
- 프로퍼티 이름 앞에 `readonly`를 넣어서 이를 지정할 수 있다.
- 배열 같은 경우는 `ReadonlyArray`를 사용한다.
  > 타입 단언으로 오버라이드하는 것은 가능하다.
- 변수는 `const` 프로퍼티는 `readonly`를 사용한다

## 초과 프로퍼티 검사(Excess Property Checks)

- 객체 리터럴은 다른 변수에 할당할 때나 인수로 전달할 때, 특별한 처리를 받고, `초과 프로퍼티 검사`를 받는다. 만약 객체 리터럴이 대상 타입이 갖고 있지 않은 프로퍼티를 갖고 있으면 에러가 발생한다.

```typescript
// error: Object literal may only specify known properties, but 'colour' does not exist in type 'SquareConfig'. Did you mean to write 'color'?
let mySquare = createSquare({ colour: "red", width: 100 });
```

- 초과 프로퍼티 검사를 피하는 방법은 타입 단언을 사용하는 것이다.

```typescript
let mySquare = createSquare({ width: 100, opacity: 0.5 } as SquareConfig);
```

- 추가 프로퍼티가 있음을 확신한다면 문자열 인덱스 서명을 추가하는 것이 더 나은 방법이다.
- 추가 프로퍼티 검사를 피하는 다른 방법은 다른 변수에 할당 하는것이다.
  > 만약 공통 객체 프로퍼티가 없으면 에러가 발생한다.

```typescript
let squareOptions = { colour: "red", width: 100 };
let mySquare = createSquare(squareOptions);
```

## 인덱서블 타입(Indexable Types)

- `a[10]`이나 `ageMa["diniel"]`처럼 타입을 `인덱스`로 기술할 수 있다.
- 인덱서블 타입은 인덱싱 할때 해당 반환 유형과 함께 객체를 인덱싱하는 데 사용할 수 있는 타입을 기술하는 `인덱스 시그니처`를 가지고있다.
- 인덱스의 할당을 막기 위해 인덱스 시그니처를 `읽기 전용`으로 만들 수 있다.
- 문자열 인덱스 시그니처는 사전패턴을 기술하는데 강력한 방법이지만, 모든 프로퍼티들이 반환 타입과 일치하도록 강제합니다.

```typescript
interface NumberDictionary {
  [index: string]: number;
  length: number; // 성공, length는 숫자입니다
  name: string; // 오류, `name`의 타입은 인덱서의 하위타입이 아닙니다
}

interface NumberOrStringDictionary {
  [index: string]: number | string;
  length: number; // 성공, length는 숫자입니다
  name: string; // 성공, name은 문자열입니다
}
```

## 클래스 타입(Class Types)

- 클래스는 두 가지 타입을 가진다. (스태틱 타입과 인스턴스 타입)

## 인터페이스 확장하기

- 인터페이스들도 확장이 가능하다. 이는 한 인터페이스의 멤버를 다른 인터페이스에 복사하는 것을 가능하게 해주는데, 인터페이스를 재사용성 높은 컴포넌트로 쪼갤 때, 유연함을 제공한다.
- 인터페이스는 여러 인터페이스를 확장할 수 있어, 모든 인터페이스의 조합을 만들어 낼 수 있다.

```typescript
interface Shape {
  color: string;
}

interface PenStroke {
  penWidth: number;
}

interface Square extends Shape, PenStroke {
  sideLength: number;
}

let square = {} as Square;
square.color = "blue";
square.sideLength = 10;
square.penWidth = 5.0;
```
