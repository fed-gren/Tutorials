# Jest

## 02. Matchers 사용하기

jest에서는 다양한 방법으로 값들을 테스트 할 수 있는데, 이를 `matchers`라고 부릅니다. `시작하기`에서 보았던 toBe 또한 matcher입니다.

<br />

---

### 기본 Matchers

expect와 toBe를 사용해서 원시값(primitive value)이 같은지 테스트할 수 있습니다.
```js
test("2 더하기 2는 4죠.", () => {
  expect(2 + 2).toBe(4);
});
```
위 코드를 실행하면 expect(2 + 2)는 `expectation` 객체를 반환합니다. toBe는 matcher이고, expect에서 계산한 값과 matcher의 인자로 있는 값을 비교하여 실패한 경우 에러 메시지를 출력합니다.

`toBe`는 정확한 테스트를 위해 `Object.is`를 사용합니다.
`Note` Object.is는 내장 메서드로, 인자로 들어온 두 값이 같은지를 비교해서 `Boolean`으로 반환합니다.

따라서 객체 내부 속성과 값이 같은지를 비교하려면 `toBe`로는 불가능하고, `toEqual`을 사용해야 합니다.
```js
test('object assignment), () => {
  const data = {one: 1};
  data['two'] = 2;
  expect(data).toEqual({one: 1, two: 2});
});
```
`toEqual`은 배열이나 객체의 모든 값이 같은지 재귀적으로 확인합니다.

`not`을 사용하여 값이 같지 않은 경우를 테스트 할 수도 있습니다.
```js
test("2 더하기 2는 5가 아니죠!", () => {
  expect(2 + 2).not.toBe(5);
});
//PASS
```

<br />

## 참고

- jest - [Using matchers](https://jestjs.io/docs/en/using-matchers)