# CSS Modules: Values

Pass arbitrary values between your module files, transforms

```css
@value primary: #BF4040;
@value secondary: #1F4F7F;
```

into

```css
:export {
  primary: #BF4040;
  secondary: #1F4F7F;
}
```

### Usage

```css
/* colors.css */
@value primary: #BF4040;
@value secondary: #1F4F7F;

.text-primary {
  color: primary;
}

.text-secondary {
  color: secondary;
}
```

```css
/* breakpoints.css */
@value small: (max-width: 599px);
@value medium: (min-width: 600px) and (max-width: 959px);
@value large: (min-width: 960px);
```

```css
/* my-component.css */
/* alias paths for other values or composition */
@value colors: "./colors.css"; 
/* import multiple from a single file */
@value primary, secondary from colors;
/* make local aliases to imported values */
@value small as bp-small, large as bp-large from "./breakpoints.css";

.header {
  composes: text-primary from colors;
  box-shadow: 0 0 10px secondary;
}

@media bp-small {
  .header {
    box-shadow: 0 0 4px secondary;
  }
}
@media bp-large {
  .header {
    box-shadow: 0 0 20px secondary;
  }
}
```

**If you are using Sass** along with this PostCSS plugin, do not use the colon `:` in your `@value` definitions. It will cause Sass to crash.

Note also you can _import_ multiple values at once but can only _define_ one value per line.

```css
@value a: b, c: d; /* defines a as "b, c: d" */
```

### Justification

See [this PR](https://github.com/css-modules/css-modules-loader-core/pull/28) for more background

## License

ISC

## With thanks

- Mark Dalgleish
- Tobias Koppers
- Josh Johnston

---
Glen Maddern, 2015.
