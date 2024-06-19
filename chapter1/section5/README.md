# 유니언과 교차 타입

## 유니언 타입

- 여러 타입중 하나가 될 수 있는 값을 의미한다. `|`
  > number | string | boolean은 값의 타입이 number, string, boolean이 될 수 있음을 의미한다.

## 공통 필드를 갖는 유니언

- 유니언에 있는 모든 타입에 공통인 멤버들에만 접근할 수 있다.
- 아래 예시의 경우 `layEggs()`에만 접근이 가능하다.

```typescript
interface Bird {
  fly(): void;
  layEggs(): void;
}

interface Fish {
  swim(): void;
  layEggs(): void;
}

declare function getSmallPet(): Fish | Bird;
```

## 교차 타입

- 교차 타입은 여러 타입을 하나로 결합한다. `&`
- 예를 들어, `Person & Serializable & Loggable`은 Person 과 Serializable 그리고 Loggable입니다. 즉, 이 타입의 객체는 세 가지 타입의 모든 멤버를 갖게 됩니다.
