# SCSS Boxes Project

### 0. 기초 HTML

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Boxes</title>
    <link rel="stylesheet" href="css/index.css" />
  </head>
  <body>
    <h1>Boxes</h1>

    <div class="box">
      <div class="box-inner">
        <div class="box-inner-title">box-inner-1</div>
      </div>
      <div class="box-inner">
        <div class="box-inner-title">box-inner-2</div>
      </div>
      <div class="box-inner">
        <div class="box-inner-title">box-inner-3</div>
      </div>
    </div>
  </body>
</html>

```

### 1. Nesting 코드 구조화

```scss

.box .box-inner {
  background-color: #ccc;
}

.box .box-inner .box-inner-title {
  font-size: 20px;
}

```

```scss
// nesting

.box {
  .box-inner {
    background-color: #ccc;

    .box-inner-title {
      font-size: 20px;
    }
  }
}
```

### 2. 중복 코드 &

```scss

.box {
  border: 3px solid #000;

  .box-inner {
    border: 3px solid #000;
    background-color: #ccc;
    .box-inner-title {
      font-size: 20px;
    }
  }
}

```

```scss

.box {
  &,
  &-inner {
    border: 5px solid #000;
  }
  // .box
  &-inner {
    background-color: #ccc;
    // .box-inner-title
    &-title {
      font-size: 20px;
    }
  }
}


```

### 3. 변수

```scss
// var
$color-white: #fff;
$color-black: #000;
$color-gray: #ccc;
$color-gray-light: #efefef;
$color-red: #f00;
$color-blue: #00f;

$border-color: $color-blue;

body {
  margin: 0;
  background-color: $color-gray-light;
  font-family: sans-serif;
}

.box {
  width: 300px;
  height: 300px;
  padding: 20px;

  &,
  &-inner {
    border: 3px solid $border-color;
  }
  // .box
  &-inner {
    padding: 10px;
    height: 40px;
    background-color: $color-gray;
    // .box-inner-title
    &-title {
      font-size: 20px;
      color: $color-white;
      background-color: rgba($color-black, 0.5);
    }
  }
}

```

### 4. Mixin

```scss
// var
$color-white: #fff;
$color-black: #000;
$color-gray: #ccc;
$color-gray-light: #efefef;
$color-red: #f00;
$color-blue: #00f;
$border-color: $color-blue;

// mixin
@mixin width-height-padding($width, $height, $padding) {
  width: $width;
  height: $height;
  padding: $padding;
}

body {
  margin: 0;
  background-color: $color-gray-light;
  font-family: sans-serif;
}

.box {
  // width: 300px;
  // height: 300px;
  // padding: 20px;
  @include width-height-padding(300px, 300px, 20px);

  &,
  &-inner {
    border: 3px solid $border-color;
  }
  // .box
  &-inner {
    @include width-height-padding(initial, 40px, 10px);
    // height: 40px;
    // padding: 10px;
    background-color: $color-gray;
    // .box-inner-title
    &-title {
      font-size: 20px;
      color: $color-white;
      background-color: rgba($color-black, 0.5);
    }
  }
}

```

### 5. Mixin - Center

```scss
@mixin pos-abs-center() {
  position: absolute;
  left: 50%;
  top: 50%;
  // translate 는 자기자신의 넓이를 중심으로 움직이게 됩니다.
  transform: translate(-50%, -50%);
}

@mixin pos-abs-center-horizontal() {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

@mixin pos-abs-center-vertical() {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```

### 6. Partial

```scss
// variables.scss

$color-white: #fff;
$color-black: #000;
$color-gray: #ccc;
$color-gray-light: #efefef;
$color-red: #f00;
$color-blue: #00f;
$border-color: $color-blue;
```

```scss
// mixins.scss

@mixin width-height-padding($width, $height, $padding) {
  width: $width;
  height: $height;
  padding: $padding;
}

@mixin pos-abs-center() {
  position: absolute;
  left: 50%;
  top: 50%;
  // translate 는 자기자신의 넓이를 중심으로 움직이게 됩니다.
  transform: translate(-50%, -50%);
}

@mixin pos-abs-center-horizontal() {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

@mixin pos-abs-center-vertical() {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}

```

```scss
@import "abstracts/variables";
@import "abstracts/mixins";

body {
  margin: 0;
  background-color: $color-gray-light;
  font-family: sans-serif;
}

.box {
  // width: 300px;
  // height: 300px;
  // padding: 20px;
  @include width-height-padding(300px, 300px, 20px);
  @include pos-abs-center();

  &,
  &-inner {
    border: 3px solid $border-color;
  }
  // .box
  &-inner {
    @include width-height-padding(initial, 40px, 10px);
    // height: 40px;
    // padding: 10px;
    background-color: $color-gray;
    // .box-inner-title
    &-title {
      font-size: 20px;
      color: $color-white;
      background-color: rgba($color-black, 0.5);
    }
  }
}

```

### 7. Media

- Desktop-big : 1201 이상
- Desktop : 901 ~ 1200
- Tablet : 601 ~ 900
- Phone : 600 이하

```scss
// css
// desktop-big
@media screen and (min-width: 1201px) {
  .box {
    border: 10px solid $border-color;
  }
}
// tablet
@media screen and (min-width: 601px) and (max-width: 900px) {
  .box {
    border: 1px solid $border-color;
  }
}
//phone
@media screen and (max-width: 600px) {
  .box {
    border: none;
  }
}
```

```scss
// _mixin.scss

@mixin mq($screen-width) {
  @if $screen-width == "phone" {
    @media screen and (max-width: 600px) {
      @content;
    }
  } @else if $screen-width == "tablet" {
    @media screen and (min-width: 601px) and (max-width: 900px) {
      @content;
    }
  } @else if $screen-width == "desktop-big" {
    @media screen and (min-width: 1201px) {
      @content;
    }
  } @else {
    // desktop
  }
}

```

```scss
@import "abstracts/variables";
@import "abstracts/mixins";
@import "base/base";

.box {
  @include width-height-padding(300px, 300px, 20px);
  @include pos-abs-center();

  &,
  &-inner {
    border: 3px solid $border-color;
  }

  @include mq("phone") {
    width: 100%;
    border: none;
  }
  @include mq("tablet") {
    border: 2px solid $border-color;
  }
  @include mq("desktop-big") {
    border: 10px solid $border-color;
  }

  &-inner {
    @include width-height-padding(initial, 40px, 10px);
    background-color: $color-gray;

    @include mq("desktop-big") {
      width: 300px;
      height: 70px;
    }

    &-title {
      font-size: 40px;
      color: $color-white;
      background-color: rgba($color-black, 0.5);

      @include mq("phone") {
        font-size: 20px;
      }
      @include mq("tablet") {
        font-size: 30px;
      }
      @include mq("desktop-big") {
        font-size: 50px;
      }
    }
  }
}

```

