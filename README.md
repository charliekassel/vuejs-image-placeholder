# Vuejs Image Placeholder

> svg image placeholder

Creates a customisable svg image placeholder

## Install

```bash
npm install vuejs-image-placeholder
```

## Usage

All props are optional

Basic
```html
<image-placeholder
    :width="200"
    :height="200"
    :background-colour="#ddd"
    :border-colour="#000"
    :border-width="2"
    :show-ratio="true"
    :font-family="Tahoma, sans-serif"
    :font-colour="#333"
    :font-size="18"
></image-placeholder>
```


## Available props

|Prop              |Type    |Default  |Description|
|------------------|--------|---------|----------|
|width             |Number  |200      |Img width |
|height            |Number  |150      |Img height|
|backgroundColour  |String  |#ccc     |Background colour|
|borderColour      |String  |#333     |Border colour|
|borderWidth       |Number  |1        |Border width|
|showRatio         |Boolean |false    |Show image size in pixels or the proportion ratio|
|fontFamily        |String  |monospace|Font for the display text|
|fontColour        |String  |#333     |Display text colour|
|fontSize          |Number  |14       |Display text size|
