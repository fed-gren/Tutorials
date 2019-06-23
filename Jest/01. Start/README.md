# Jest

## 01. 시작하기

jest를 사용해 테스트하고자 하는 프로젝트에서 jest를 설치합니다.
- `yarn`을 사용한 방법
```sh
yarn add --dev jest
```

- `npm`을 사용한 방법
```sh
npm install --save-dev jest
```

아주 기본적인 테스트를 진행해보겠습니다. 두 수를 인자로 받아 그 합을 반환하는 함수를 테스트 하기 위해, `sum.js`라는 파일을 생성합니다.

```js
const sum = (a, b) => a + b;
module.exports = sum;
```

그 다음, `sum`함수를 테스트하기 위한 테스트 파일을 `sum.test.js`라고 생성합니다.
```js
const sum = require("./sum");

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

`package.json`의 scripts에 아래 내용을 추가합니다.
```json
{
  "scripts": {
    "test": "jest"
  }
}
```
이제 `yarn test`라고 입력하면 jest로 테스트한 결과를 확인할 수 있습니다.

```sh
❯ yarn test
yarn run v1.9.4
$ jest
 PASS  Examples/01. Start/sum.test.js
  ✓ adds 1 + 2 to equal 3 (3ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.664s
Ran all test suites.
✨  Done in 2.92s.
```

위는 직접 테스트를 실행했을 때 출력되는 결과입니다.

제일 먼저 yarn test라고 입력했을 때 스크립트에서 jest를 실행하라고 했기 때문에 jest 명령어를 알아서 입력해 줬습니다.

결과로는 PASS라고 나왔지만 테스트가 끝나기 전엔 RUN이라고 나오고 테스트가 통과하자 PASS라고 바뀌었습니다.

그리고 테스트 코드(sum.test.js)에서 작성했던 `adds 1 + 2 to equal 3`가 출력되었습니다. 이처럼 test 함수 내에 첫 번째 인자로 준 메세지를 통해 어떤 테스트가 통과되었고, 실패했는지를 빠르게 파악할 수 있습니다.

아래에는 전체 테스트에 대한 통계입니다. Test Suites는 테스트 그룹을 의미합니다.
Tests는 말 그대로 몇개의 테스트가 통과했고 실패했는지 보여줍니다.
Snapshots은 결과값을 파일로 저장해서 테스트 할 때마다 테스트 결과값을 파일의 결과값과 비교하는 것입니다.

위 기본 테스트에서는 `expect`와 `toBe` 메서드를 사용해서 결과값이 정확한지 테스트했습니다. jest에서는 기대값과 결과값을 비교하는 함수들을 통틀어 `Mathers`라고 부릅니다.

<br />

---

### CLI를 통해 테스트하기

jest가 PATH에 추가되어 있는 경우(global하게 사용가능), CLI에서 Jest를 직접 실행시킬 수 있습니다.
```sh
jest sum
```

<br />

---

### 설정 추가하기

#### 기본 설정 파일 생성하기

아래 명령어를 사용하면 프로젝트에 적합한 테스트 설정을 위한 몇가지 질문이 나옵니다. 프로젝트에 맞게 선택하면 `jest.config.js`파일이 생성됩니다.

<br />

---

## 참고

- [Jest Get Strated](https://jestjs.io/docs/en/getting-started.html)