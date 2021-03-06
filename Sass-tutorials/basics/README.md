# Sass Basics

## Sass의 필요성

웹 애플리케이션의 구조가 커지고 복잡해짐에 따라 CSS 파일 또한 복잡해져 이를 관리, 유지보수하기가 어려워집니다. 이러한 문제점을 해결하기 위해 CSS preprocessor(전처리기)가 등장했습니다. Sass가 preprocessor의 일종입니다.

Sass를 사용하면 변수, nesting, mixins, 상속 등의 기능 들을 사용하여 편리하게 Stylesheet를 작성하고 관리할 수 있습니다.

<br/>

---

## Preprocessing

Sass를 설치하면 sass 명령어를 사용해 sass를 css로 컴파일할 수 있습니다. 사용자는 sass에게 어떤 파일을 빌드해야 하는지, 그리고 css를 어디서 출력해야 하는지 작성하면 됩니다.

예를 들어 터미널에서 sass input.scss output.css를 실행하면 input.scss를 읽어 컴파일 한 뒤 output.css로 만듭니다.

--watch 옵션을 통해 파일 혹은 디렉토리를 감시 할 수 있습니다. watch는 sass에게 원본 파일의 변경 사항을 감시하고 sass를 저장할 때마다 css파일로 다시 컴파일할 수 있게 해줍니다. input.scss 파일을 수동으로 빌드하지 않고 감시하려면 아래와 같이 watch 옵션을 명령어에 추가합니다.

```sh
sass --watch input.scss output.css
```

폴더 경로를 입력, 출력에 입력(콜론으로 구분)하고 디렉토리에 대해 감시할 수 있습니다.

```sh
sass --watch app/sass:public/stylesheets
```

Sass는 app/sass 폴더에 있는 모둔 파일의 변화에 대해 감시하고 CSS 파일로 컴파일해서 public/stylesheets 폴더에 저장할 것입니다.

<br/>

---

## 변수 (Variables)

변수는 재사용하기 원하는 정보를 저장할 때 아주 유용합니다. 폰트, 폰트 색상 등과 같은 CSS의 모든 값을 재사용할 수 있습니다. Sass에서 `$`를 사용하여 변수를 만들 수 있습니다.

아래 예시는 변수를 사용하여 작성한 scss 파일과 이 scss 파일을 컴파일한 css 파일의 내용입니다.

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```

<br/>

---

## 중첩 (Nesting)

Nesting은 `둥지를 튼다`는 의미입니다. Sass에서는 자식 태그에 스타일을 줄 때 부모 태그에 둥지를 튼 듯한 형태로 스타일을 작성하면 자식 태그에 적용됩니다.

HTML을 작성 할 때, 부모 자식 관계는 중첩에 의해 시각적으로 계층 구조를 확인할 수 있지만 일반적인 CSS에서는 그렇지 않습니다.

Sass는 HTML의 동일한 시각적 계층구조를 따르는 방식으로 CSS 선택자에 중첩이 가능하게 해줍니다.(중첩은 부모-자식 관계를 의미합니다.) 하지만 지나치게 중첩된 구조는 유지보수가 어렵기 때문에 좋은 구조는 아니라는 점을 기억해야 합니다.

아래는 중첩구조의 Sass와 컴파일 된 CSS 예시입니다.

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

<br/>

---

## Partials

Sass 파일을 작게 나누어 모듈화 할 수 있습니다. 모듈로 사용하고자 나눈 파일명은 \_partial.scss와 같이 밑줄(\_)로 시작하도록 작성합니다. 파일명 앞에 밑줄(\_)이 있어야 Sass가 이 파일이 모듈임을 알고 단독 CSS 파일로 컴파일 하지 않습니다.

이 모듈은 다른 sass 파일에서 @import로 불러서 사용합니다.

<br/>

---

## Import

CSS에서 유지 보수를 좀 더 편하게 하기 위해 CSS를 가져오는 옵션이 있습니다. 이 방법의 단점은 CSS에서 @import를 사용할 때마다 새로운 HTTP 요청을 만든다는 점입니다.

Sass는 CSS @import 기반으로 구성되지만 HTTP 요청을 새로 만들지 않고, 단일 CSS 파일을 웹 브라우저에게 제공할 수 있도록 파일들을 결합합니다.

아래 예시는 \_reset.scss를 base.scss로 불러와 사용하는 예시입니다.

**\_reset.scss**

```scss
html,
body,
ul,
ol {
  margin: 0;
  padding: 0;
}
```

**base.scss**

```scss
@import "reset";
body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```

**base.css**

```css
html,
body,
ul,
ol {
  margin: 0;
  padding: 0;
}
body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```

<br/>

---

## Mixins

Mixin은 재사용하기 위한 css 선언 그룹을 만들수 있는 기능입니다. mixin은 함수처럼 값을 입력받도록 만들어 유연하게 사용할 수 있습니다.

Mixin은 `@mixin`으로 선언하고, `@include`로 사용합니다. 파라미터를 정의할 땐 변수를 사용했을 때와 같이 \$에 변수명을 붙입니다.

**Sass**

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}
.box {
  @include transform(rotate(30deg));
}
```

**CSS**

```css
.box {
  -webkit-transform: rotate(30deg);
  -ms-transform: rotate(30deg);
  transform: rotate(30deg);
}
```

<br/>

---

## Extend/Inheritance

상속은 Sass에서 가장 유용한 기능 중 하나입니다. `@extend`를 사용하면 한 선택자에서 다른 선택자로 CSS 속성을 공유할 수 있습니다.
아래 예시 코드는 상속을 사용해서 errors, warnings, successes 메시지 스타일 속성을 지정해주는 코드입니다.

```scss
/* This CSS will print because %message-shared is extended. */
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

// This CSS won't print because %equal-heights is never extended.
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
```

```css
/* This CSS will print because %message-shared is extended. */
.message,
.success,
.error,
.warning {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  border-color: green;
}

.error {
  border-color: red;
}

.warning {
  border-color: yellow;
}
```

위 코드에서 message, success, error, warning 클래스를 가진 요소들이 %message-shared 스타일을 공통적으로 가진다는 것을 알 수 있습니다. 상속 받은 스타일 외 각 클래스 별로 부여한 스타일 속성은 따로 적용되었습니다. 이처럼 상속을 사용하면 HTML 요소에 여러 개의 클래스명을 작성하지 않아도 된다는 이점이 있습니다.

참고로 %equal-heights 관련 속성은 CSS에 나타나지 않았는데, 이는 %equal-heights를 상속받아 사용하지 않았기 때문입니다.

<br/>

---

## Operators

Sass에서는 간단한 연산자(+, -, \*, /, %)를 사용하여 스타일 속성 값을 적용시켜줄 수 있습니다. 아래 예시는 aside, article 요소의 너비를 계산하기 위한 코드입니다.

```scss
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```

```css
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 62.5%;
}

aside[role="complementary"] {
  float: right;
  width: 31.25%;
}
```

<br/>

---

## 참고

- [Sass Basics](https://sass-lang.com/guide)
