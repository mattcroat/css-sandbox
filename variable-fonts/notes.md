# Variable Fonts

[How to use variable fonts in the real world](<https://medium.com/clear-left-thinking/how-to-use-variable-fonts-in-the-real-world-e6d73065a604>)

### index.html
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Variable Fonts</title>
  <link rel="stylesheet" href="main.css">
</head>

<body>

  <h1 class="anim1">MAXIMUM OVERLOAD</h1>
  <span class="anim1">And this is a subheadline.</span>

</body>

</html>
```

### main.css
```scss
/* @font-face for variable font */
@font-face {
  font-family: 'Gingham';
  src: url('Gingham.woff2') format('woff2');
}

* {
  margin: 0;
  padding: 0;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

html {
  box-sizing: border-box;
  font-size: 62.5%;
}

body {
  font-size: 1.6rem;
  /* Variable font in action */
  font-family: 'Gingham', sans-serif;
  padding: 8rem;
}

h1 {
  font-variation-settings: 'wght' 700, 'wdth' 400;
  font-size: 10rem;
}

span {
  /* Variable font settings */
  font-variation-settings: 'wght' 0, 'wdth' 0;
  font-size: 6rem;
  text-transform: uppercase;
}

.anim1 {
  animation: anim1 2s infinite alternate;
}

/* Animation keyframes */
@keyframes anim1 {
  from {
    font-variation-settings: 'wght' 0, 'wdth' 0;
  }
  to {
    font-variation-settings: 'wght' 700, 'wdth' 150;
  }
}
```

## Fallback

Firstly we gave the variable font a different name to the single-style typeface, thus separating links to variable fonts from single-style fonts:

```scss
@font-face {
  font-family: 'GinghamVariable';
  src: url('gingham-variable.woff2') format('woff2');
  font-weight: 1 999;
}

@font-face {
  font-family: 'Gingham';
  src: url('gingham-black.woff2') format('woff2'),
         url('gingham-black.woff') format('woff');
  font-weight: 900; 
}

@font-face {
  font-family: 'Gingham';
  src: url('gingham-semibold.woff2') format('woff2'),
         url('gingham-semibold.woff') format('woff');
  font-weight: 600; 
}
```

We then needed to write an @supports rule to ensure the right fonts went to the right browsers:

```scss
html {
  font-family: 'Gingham' sans-serif;
}

@supports (font-variation-settings: normal) {
  html {
    font-family: 'GinghamVariable', sans-serif;
  }
}
```

In the above code, the single-style fonts are specified as standard, however if a browser supports variable fonts (it’s a reasonable assumption that can be judged by support for font-variation-settings) then it gets the variable font instead.