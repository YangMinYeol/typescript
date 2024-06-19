# 리터럴 타입

- 리터럴 타입은 `문자열 리터럴 타입`과 `숫자형 리터럴 타입` 두 가지가 있디.

## 문자열 리터럴 타입

- 문자열 리터럴 타입은 유니언 타입, 타입 가드 그리고 타입 별칭과 잘 결합된다.

```typescript
type Easing = "ease-in" | "ease-out" | "ease-in-out";
```

## 숫자형 리터럴 타입

- 숫자형 리터럴 타입은 주로 설정값을 설명할 때 사용된다.

```typescript
interface MapConfig {
  lng: number;
  lat: number;
  tileSize: 8 | 16 | 32;
}
```
