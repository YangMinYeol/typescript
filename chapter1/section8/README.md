# 제네릭

- 함수에 타입 인수를 포함한 모든 인수를 전달할 수 있다.
  > let output = identity<string>("myString"); // 출력 타입은 'string'입니다.
- 전달하는 인수에 따라서 컴파일러가 `T`의 값을 자동으로 정하게 한다.
  > let output = identity("myString"); //출력 타입은 'string'입니다.

```typescript
function identity<T>(arg: T): T {
  return arg;
}
```
