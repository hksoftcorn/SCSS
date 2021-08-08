# LoremProject

## 1. CSS의 기초

### 1.1. 기본단위 em & rem

- em : 해당 요소에 적용된 글자크기를 기본으로 한 size입니다.
  - 기본 font-size: 16px입니다.
- rem : root에 지정된 font-size를 기본으로 한 size입니다.

```scss
html {
  // font-size: 10px;
  font-size: 62.5%; // 10px
}

#box-1 {
  font-size: 3rem; // 1em = 20px;
  width: 20rem;
  background-color: #aaa;
}

#box-2 {
  font-size: 2rem;
  width: 20rem; //
  background-color: #777;
}
```

### 1.2. 기본단위 vw & vh

- vw : 현재 보고있는 화면 너비
- vh : 현재 보고있는 화면 높이





## 2. Project 구성하기

### 2.1. 기초설정

- font 설정
- 전체 속성 설정
- html 10px 설정

```scss
// google font
@import url("https://fonts.googleapis.com/css2?family=Nanum+Gothic:wght@400;700;800|Lato:wght@100;300&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%; // 10px => 1rem
}

body {
  font-family: "Nanum Gothic", sans-serif;
}
```



### 2.2. 헤더 작업

- 제목 글자 위치 고정&맞추기
  - 부모태그는 relative로, 자식태그는 absolute로 해야 정확하게 맞춰집니다.

```scss

header {
  width: 100%;
  height: 90vh;
  position: relative;

  #logo-text {
    position: absolute;
    left: 7rem;
    top: 4rem;
    font-size: 5.6rem;
    text-transform: uppercase;
    font-family: "Lato", sans-serif;
    font-weight: 100;
  }
  #header-text {
    &-main {
      font-size: 30px;
    }
    &-sub {
      font-size: 20px;
    }
  }
}
```

- 배경 이미지 작업하기
  - 배경이미지 설정하기
  - 배경이미지를 cover로 박스에 꽉차게 설정하기
  - 그라디언트 적용하기

```scss

header {
  ...
  background-image: linear-gradient(to right, #285a91 0%, #1f9cfd 100%),
    url(../images/header-image.jpg);
  background-size: cover;
  background-blend-mode: multiply;

```

- 헤더 제목 + 내용 위치 고정&맞추기

```scss
// google font
@import url("https://fonts.googleapis.com/css2?family=Nanum+Gothic:wght@400;700;800&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Lato:wght@100;300&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  padding: 3rem;
  font-size: 62.5%; // 10px => 1rem
}

body {
  font-family: "Nanum Gothic", sans-serif;
}

header {
  width: 100%;
  height: 90vh;
  background-image: linear-gradient(to right, #285a91 0%, #1f9cfd 100%),
    url(../images/header-image.jpg);
  background-blend-mode: multiply;
  background-size: cover;
  position: relative;

  #logo-text {
    position: absolute;
    left: 7rem;
    top: 4rem;
    font-size: 5.6rem;
    text-transform: uppercase;
    font-family: "Lato", sans-serif;
    font-weight: 100;
    color: #fff;
    letter-spacing: -0.5rem;
  }
  #header-text {
    position: absolute;
    left: 7rem;
    bottom: 23%;
    color: #fff;
    letter-spacing: -0.1rem;
    font-weight: 700;

    &-main {
      font-size: 7.2rem;
      line-height: 7.2rem;
    }
    &-sub {
      margin-top: 3rem;
      font-size: 2.4rem;
    }
  }
}

```



### 2.3. Animation과 Transtion

#### Transtion

```scss
// transtion
.btn {
  font-size: 30px;
  text-decoration: none;
  opacity: 1;
  transition: all 5s;
  // transition: font-size 5s;

  &:hover {
    font-size: 50px;
    text-decoration: underline;
    opacity: 0.2;
  }
}

```

#### Animation

```scss
// animation
@keyframes anim1 {
  // 주어진 시간에 대한 % 입니다.
  0% {
    opacity: 0.2;
    transform: translate(100px, -30px);
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0.1;
  }
}

#box1 {
  animation-name: anim1;
  animation-duration: 5s;
  // 애니메이션의 마지막 모드를 남아있도록 해줍니다.
  animation-fill-mode: forwards;
  // delay가 지정되었을때, 마지막 모드로 시작하도록 합니다.
  animation-fill-mode: backwards;
  animation-delay: 3s;
  // forwards와 backwards 둘 다 지정합니다.
  animation-fill-mode: both;
}

```

```scss
// animation
@keyframes moveInLeft {
  0% {
    opacity: 0.1;
    transform: translateX(-8rem);
  }
  80% {
    transform: translateX(1rem);
  }
  100% {
    opacity: 1;
    transform: translate(0);
  }
}
@keyframes moveInRight {
  0% {
    opacity: 0.1;
    transform: translateX(10rem);
  }
  80% {
    transform: translateX(-1rem);
  }
  100% {
    opacity: 1;
    transform: translate(0);
  }
}
...

#logo-text {
	...
    animation-name: moveInLeft;
    animation-duration: 1s;
    // animation-iteration-count: 3;
    animation-fill-mode: backwards;
    animation-delay: 2s;
  }

    &-main {
      font-size: 7.2rem;
      line-height: 7.2rem;
      animation-name: moveInRight;
      animation-duration: 1s;
      animation-delay: 0.5s;
      animation-fill-mode: backwards;
    }
    &-sub {
      margin-top: 3rem;
      font-size: 2.4rem;
      animation-name: moveInRight;
      animation-duration: 1s;
      animation-delay: 1s;
      animation-fill-mode: backwards;
    }
  }
}

```



### 2.4. Partial

- abstracts : Sass가 제공하는 기능적인 것들에 대한 정의
  - `@mixin`과 `변수` 와 같은 CSS로 구체적 변환 전 추상적 정의들
- base : CSS의 기본적이고 기능적인 설정들
- components : 버튼이나 메뉴같은 마우스 컨트롤 요소들
  - a / button / nav
- layout : 페이지 내용 구성에 따른 각 부분별 요소
  - header / main / footer

```scss
// index.scss
@import "base/base";
@import "base/animations";
@import "abstracts/variables";
@import "layout/header";
```

```scss
// base/_base.scss

// google font
@import url("https://fonts.googleapis.com/css2?family=Nanum+Gothic:wght@400;700;800&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Lato:wght@100;300&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  padding: 3rem;
  font-size: 62.5%; // 10px => 1rem
}

body {
  font-family: "Nanum Gothic", sans-serif;
}

```

```scss
// base/_animations.scss
@keyframes moveInLeft {
  0% {
    opacity: 0.1;
    transform: translateX(-8rem);
  }
  80% {
    transform: translateX(1rem);
  }
  100% {
    opacity: 1;
    transform: translate(0);
  }
}
@keyframes moveInRight {
  0% {
    opacity: 0.1;
    transform: translateX(10rem);
  }
  80% {
    transform: translateX(-1rem);
  }
  100% {
    opacity: 1;
    transform: translate(0);
  }
}

```

```scss
// abstracts/_variables.scss

$color-white: #fff;
$color-primary: #285a91;
$color-secondary: #1f9cfd;
```

```scss
// layout/_header.scss

header {
  width: 100%;
  height: 90vh;
  background-image: linear-gradient(to right, $color-primary 0%, $color-secondary 100%),
    url(../images/header-image.jpg);
  background-blend-mode: multiply;
  background-size: cover;
  position: relative;

  #logo-text {
    position: absolute;
    left: 7rem;
    top: 4rem;
    font-size: 5.6rem;
    text-transform: uppercase;
    font-family: "Lato", sans-serif;
    font-weight: 100;
    color: $color-white;
    letter-spacing: -0.5rem;

    animation-name: moveInLeft;
    animation-duration: 1s;
    // animation-iteration-count: 3;
    animation-fill-mode: backwards;
    animation-delay: 2s;
  }
  #header-text {
    position: absolute;
    left: 7rem;
    bottom: 23%;
    color: $color-white;
    letter-spacing: -0.1rem;
    font-weight: 700;

    &-main {
      font-size: 7.2rem;
      line-height: 7.2rem;
      animation-name: moveInRight;
      animation-duration: 1s;
      animation-delay: 0.5s;
      animation-fill-mode: backwards;
    }
    &-sub {
      margin-top: 3rem;
      font-size: 2.4rem;
      animation-name: moveInRight;
      animation-duration: 1s;
      animation-delay: 1s;
      animation-fill-mode: backwards;
    }
  }
}

```



## 3. Pseudo

### 3.1. clearfix (anti float)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="css/pseudo.css" />
  </head>
  <body>
    <div id="box">box</div>
    <div class="box-parent">
      <div class="box-child"></div>
      <div class="box-child"></div>
      <div class="box-child"></div>
      <div class="clearfix"></div>
    </div>
  </body>
</html>

```

```scss
.box-parent {
  padding: 20px;
  background-color: #00f;

  .box-child {
    width: 200px;
    height: 200px;
    background-color: #f00;
    border: 1px solid #ff0;
    float: left;
  }

  .clearfix {
    clear: left;
  }
}
```

```scss

.box-parent {
  padding: 20px;
  background-color: #00f;

  .box-child {
    width: 200px;
    height: 200px;
    background-color: #f00;
    border: 1px solid #ff0;
    float: left;
  }

  // .clearfix {
  //   clear: left;
  // }
  &::after {
    content: "";
    display: block;
    clear: left;
  }
}

```

```scss

@mixin clearfix() {
  &::after {
    content: "";
    display: block;
    clear: left;
  }
}

.box-parent {
  padding: 20px;
  background-color: #00f;

  .box-child {
    width: 200px;
    height: 200px;
    background-color: #f00;
    border: 1px solid #ff0;
    float: left;
  }
  @include clearfix();
}

```

### 3.2. last-child

```scss
.box-parent {
  padding: 20px;
  background-color: #00f;

  .box-child {
    width: 200px;
    height: 200px;
    background-color: #f00;
    border: 1px solid #ff0;
    float: left;
    margin-right: 50px;
  }
  .box-child:last-child {
    margin-right: 0;
  }
  @include clearfix();
}
```

```scss
@mixin clearfix() {
  &::after {
    content: "";
    display: block;
    clear: left;
  }
}


.box-parent {
  padding: 20px;
  background-color: #00f;

  .box-child {
    width: 200px;
    height: 200px;
    background-color: #f00;
    border: 1px solid #ff0;
    float: left;
  }
  .box-child:not(last-child) {
    margin-right: 50px;
  }
  @include clearfix();
}

```

### 3.3. footer

```scss
footer {
  color: $color-grey-light;
  background-color: #3f4a56;
  padding: 9rem 7rem 3rem 7rem;

  @include clearfix();
  #logo-text-footer {
    width: 25%;
    font-size: 4rem;
    font-family: "Lato", sans-serif;
    font-weight: 100;
    text-transform: uppercase;
    float: left;
  }

  #copyright {
    width: 75%;
    font-size: 1.2rem;
    float: left;

    // p:first-child
    p:nth-child(1) {
      margin-bottom: 2rem;
      word-break: break-all;
      text-align: justify;

      column-count: 3;
      column-gap: 3rem;
      column-rule-style: dashed;
      column-rule-width: 1px;
      column-rule-color: #888;
      column-width: 40px;
    }
  }
}

```









