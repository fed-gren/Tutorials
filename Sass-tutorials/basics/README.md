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
