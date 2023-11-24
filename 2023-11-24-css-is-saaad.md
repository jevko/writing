# CSS is SAAAD

CSS is Spooky Action At A Distance. The CSS acronym should expand to Complicated Style Sheets. Not just complicated -- overcomplicated -- because of bad language design. Unnecessarily complex. There are errors at CSS' foundations.

The idea of separation of content and style is good in general, the impulse is right, but I think that ultimately it goes it the wrong direction.

Perhaps it's because of the framing: you can't literally _separate_ content and style, nor do you want to. What you want is _abstraction_ of style from content. Maybe if abstraction rather than separation was the slogan, things would have been different.

Let's look at CSS from a programming language design perspective.

CSS is intentionally not a full-fledged programming language, but a Domain-Specific Language (DSL), which emphasizes styling or presentation of content. It is supposed to be particularly suited for exactly this task. <!-- but it sucks at reusability --> And indeed, it does have a multitude of specialized features that make that possible. Users can define simple or complex rules that can be applied to content to change its presentation. **The fundamental problem though is in how these rules are applied**.

The order of evaluation of the rules is idiosyncratic and overcomplicated -- it's unreasonable. It's not human-friendly. Because of that, writing CSS can feel like solving a frustrating puzzle.

As far as I understand, there are 2 main mechanisms that determine the order of application of CSS styles:

1. Cascade: source order, specificity, importance.
2. Inheritance.

These are fundamental to the language. I believe that at least the first is counterproductive. It is a fundamental mistake in the design of CSS.

Why? Let's look at an example. Given an HTML element like:

```html
<span class="a b c"></span>
```

What order will the classes be appiled in? `a` then `b` then `c`? `c` then `b` then `a`?

The answer is it could be one or the other or neither. The order cannot be decided or enforced locally by the user, but instead it is determined by a relatively complex algorithm that the user is ultimately expected to understand and follow.

The user is asked to keep track of:

* The [cascade order](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade#complete_cascade_order) described by a table of 22 rows with 8 precedence levels.
* Origin types: User-agent stylesheets, Author stylesheets (inline styles, layers, and precedence), User stylesheets, Cascade layers.
* Specificity and [selector weight categories](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#selector_weight_categories) -- 3-4 categories. We have 3 hierarchical weights, increased according to the structure of a selector.

This is asking too much. And not just of designers, but of anybody. Even the most hardcore programming languages don't have rules of precedence so complicated. Moreover, some programming languages try to reduce the number of precedence rules to minimum, acknowledging that even the most seasoned programmers struggle with keeping track of them.

What would be a better model? That's a topic for another time.
