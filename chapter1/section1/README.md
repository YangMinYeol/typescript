# 기본 타입

## 불리언(Boolean)

## 숫자(Number)

## 문자열(String)

## 배열(Array)

- 배열 타입은 두가지 방법으로 쓸 수 있다.
- 첫 번째, 배열 요소들을 나타내는 타입 뒤에 `[]`를 쓴다

```typescript
let list: number[] = [1, 2, 3];
```

- 두 번째, 제네릭 배열 타입을 쓴다.

```typescript
let list: Array<number> = [1, 2, 3];
```

## 튜플

- 튜플 타입을 사용하면, 요소의 타입과 개수가 고정된 배열을 표현할 수 있다. 단 요소들의 타입이 모두 같을 필요는 없다.

```typescript
let x: [string, number];
```

## 열거 (Enum)

- 값의 집합에 이름을 붙여줄 수 있다.
- 멤버 중 하나의 값을 수동으로 설정하여 번호를 바꿀 수 있다.
- 모든 값을 수동으로 설정할 수 있다.
- 값을 사용해 enum 멤버의 이름을 알아낼 수 있다.

```typescript
enum Color {
  Red = 1,
  Green = 2,
  Blue = 4,
}
let c: Color = Color.Green;
```

## Any

- 알지 못하는 타입을 표현해야 할때 사용한다.
  > 타입 검사를 하지 않고 값들이 컴파일 시간에 검사를 통과하길 원할때 사용한다.

## Void

- `void`는 어떤 타입도 존재할 수 없음을 나타낸다.

## Null and Undefined

- `null`과 `undefined`는 다른 모든 타입의 하위 타입이다.
  > 예를 들어 `number`같은 타입에 할당할 수 있다는 것을 의미한다.

## Never

- `never`타입은 절대 발생할 수 없는 타입을 나타낸다.
- `never`타입은 모든 타입에 할당 가능한 하위 타입이다.
- `never`를 반환하는 함수는 함수의 마지막에 도달할 수 없다.

## Object

- `object`는 원시 타입이 아닌 타입을 나타낸다.

## 타입 단언 (Type assertions)

- TypeScript보다 개발자가 값에 대해 더 잘 알고 있을때가 있다. 대게, 이런 경우는 어떤 엔티티의 실제 타입이 현재 타입보다 더 구체적일 때 발생한다.
- 타입 단언에는 두가지 형태가 있다.
- 첫 번째 `angle-bracket`문법

```typescript
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

- 두 번째 `as`문법
  > typescript를 JSX와 함께 사용할 때는, `as`스타일의 단언만 허용된다.

```typescript
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```
