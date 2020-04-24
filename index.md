# SCSS convert pixel values to rem (🔉Using functions)

SCSS is a very widely used CSS preprocesser. Selector nesting, mixins, variables are some of the most used features of SCSS. One of the most unused and underrated SCSS features is [functions](https://sass-lang.com/documentation/at-rules/function).

## Why use a function

Functions are very much like mixins, with the key difference that they just return a value and do not cause side effects. In other words, they cannot set any CSS properties. All they do is take a value, perform some computation and return the value. They are [pure functions](https://en.wikipedia.org/wiki/Pure_function).

They are a good candidate as many websites use `rem` not just to set font sizes, but other box properties too. Here, is a [good CSS Tricks article about](https://css-tricks.com/theres-more-to-the-css-rem-unit-than-font-sizing/) that. Having a handy function can make your stylesheets much more elegant, not having to visually process decimal values.

## The code

Create a new file `_functions.scss` and put it in your styles directory (Or wherever you place styles).

`_functions.scss`
```markdown
$html-font-size: 16px;

@function stripUnit($value) {
	@return $value / ($value * 0 + 1);
}

@function rem($pxValue) {
	@return #{stripUnit($pxValue) / stripUnit($html-font-size)}rem;
}
```

Then you can use it like this,

```
.component {
    font-size: rem(14px); // or rem(14)
}
```

This will set the element with `.component` class font size to the computed `0.875rem`.

![That's it?](https://imgur.com/gallery/kqGHWj0)

Yeah, that's it 💯

## How does it work, you ask?

The first function `stripUnit()` takes any value and strips the unit off. This is necessary if you wanted to perform any arithmetic operation on the value, which we do later in the `rem()` function. Notice, we add the `rem` unit back to the result of `rem()` so it can be simple used.

## Further reading

If I coouldn't convince you to use functions 😭, and you still want to use mixins. This [CSS Tricks article](https://css-tricks.com/snippets/css/less-mixin-for-rem-font-sizing/) has a simple and advanced implementation.
