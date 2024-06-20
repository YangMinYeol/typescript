# 고급 타입

## 타입 가드

##### 타입 서술어

```typescript
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
```

##### in 연산자

- `in`연산자는 타입을 좁히는 표현으로 작용한다.
- `n in x` 표현에서 n은 문자열 리터럴 타입이고, x는 유니언 타입이다

```typescript
function move(pet: Fish | Bird) {
  if ("swim" in pet) {
    return pet.swim();
  }
  return pet.fly();
}
```

##### typeof

```typescript
function padLeft(value: string, padding: string | number) {
  if (typeof padding === "number") {
    return Array(padding + 1).join(" ") + value;
  }
  if (typeof padding === "string") {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${padding}'.`);
}
```

##### instanceof

```typescript
let padder: Padder = getRandomPadder();

if (padder instanceof SpaceRepeatingPadder) {
  padder; // 타입은 'SpaceRepeatingPadder'으로 좁혀집니다
}
```

## -strictNullChecks

- 변수를 선언할 때, 자동으로 `null`이나 `undefined`를 포함하지 않는다.

## 조건부 타입

- 조건부 타입은 타입관계 검사로 표현된 조건에 따라 두가지 가능한 타입 중 하나를 선택한다.

```typescript
T extends U ? X : Y
```
