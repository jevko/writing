# Decorators: The Missing CSS Feature

This is an outline of a proposal for a feature that could be added to [CSS](https://en.wikipedia.org/wiki/CSS) to greatly simplify working with the language and make it much more pleasant to use. "Decorators" seems like a fitting name for this feature, not only because it describes what it does, but also because of its similarity to the [Python feature]((https://en.wikipedia.org/wiki/Python_syntax_and_semantics#Decorators)).

CSS was designed to enable [separation of content and style](https://en.wikipedia.org/wiki/Separation_of_content_and_presentation). This is a good idea, but perhaps it should have been called something like "[abstraction](https://en.wikipedia.org/wiki/Abstraction_(computer_science)) of style from content".

The central means of abstraction should be functional. We should be able to simply define parametrizable styling functions: 

```css
@decorator important(--color) {
  font-weight: bold;
  color: var(--color);
}
@decorator message(--vertical, --horizontal, --color: red) {
  oultine: 1px solid var(--color);
  padding: var(--vertical) var(--horizontal);
  color: red;
}
```

And apply them to HTML elements:

```html
<p style="important(blue); message(10px, 15px);">some text</p>
```

The order in which these decorators are applied should be the order in which they are specified. There should be no complex nonlocal precedence rules to keep track of.

So for example:

```html
<p style="message(10px, 15px); important(blue);">some text</p>
```

Should result in:

![blue message](img/2024-03-25-blue.gif)

<details>
<summary>Equivalent HTML code</summary>

```html
<p style="outline: 1px solid red; padding: 10px 15px; font-weight: bold; color: blue;">some text</p>
```
</details>

Whereas:

```html
<p style="important(blue); message(10px, 15px);">some text</p>
```

Should result in:

![red message](img/2024-03-25-red.gif)

<details>
<summary>Equivalent HTML code</summary>

```html
<p style="font-weight: bold; outline: 1px solid red; padding: 10px 15px; color: red;">some text</p>
```
</details>

Then we would not need [BEM](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Organizing#bem), OOCSS or any other systems for organizing CSS. All of these can be seen as attempts to bring something like the above to CSS.

# See also

* [A simpler styling model for HTML: idea and proof of concept](https://github.com/djedr/html-styling-concept)
* [The problem with CSS (video)](https://www.youtube.com/watch?v=q0Otp_W3V0Y)
* [CSS is SAAAD](https://jevko.github.io/writing/2023-11-24-css-is-saaad.html)