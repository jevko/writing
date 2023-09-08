# Whitespace in Jevko

Today I noticed [this](https://github.com/jevko/specifications/issues/1) forgotten GitHub issue about interpreting whitespace in Jevko.

Writing this to loosely explain my thinking about the treatment of whitespace in Jevko and close the issue. Back then I imagined I'd write an organized and comprehensive description, but meh, that's probably not gonna happen. Maybe better to write anything instead of nothing here.

So the point about whitespace, the interesting/distinguishing feature of Jevko is that it doesn't use whitespace as a separator. The syntax is not based around whitespace at all.

This moves the complexity of dealing with things like different standards for newlines out of a Jevko parser implementations. Yes, this is trading simplicity on one level for another, making this somebody else's problem. That's possibly most of what we do in programming. Anyway, the art is exactly in organizing the complexity, so that proper things are handled at proper levels.

So if you're using Jevko you should be aware and of the fact that it doesn't handle this complexity for you. It doesn't interpret the whitespace at all. It's not discarded, it's not used for indentation, it has no special meaning. Whitespace characters are just like other characters. The only characters that build the tree structure in Jevko are the brackets.

BTW it's incredible to me how such a simple thing seems so difficult to get across. I consistently feel like I'm doing a bad job at explaining it. It really is a simple idea.

Spaces are not syntactically significant. They are not meaningful and they are not meaningless. You give them meaning as you interpret Jevko in your software. One way to look at that is "meeh, I have to deal with that, that's stupid". That's ok. Another way to look at this is "cool, I can interpret spaces the way I want". That's also ok and that's the idea.

If you think that's stupid that you have to deal with these spaces, don't use raw Jevko. You can still take advantage of it, by using a format which handles that for you. In the original GitHub issue I linked EasyJevko for example. I'm too lazy ATM to link anything else. My goal is to finish writing this. Maybe a hypothetical next iteration will be better. IDK, I might get hit by a lightning tomorrow and lose my ability to write. That's why the rush.

But I digress.

The cool side of not having significant spaces is that you get to interpret them however you want. You can have Jevko formats where indentation matters. You can have ones where it doesn't. You can have formats where you trim space instead of splitting on it. You can have ones where you fold/collapse spaces the way HTML/XML do. See -- you get all this flexibility. And all these formats still share Jevko as the underlying syntax. You can use the same parser to get the "intermediate representation" for them. That's the value.

So the bottom line is: Jevko is a low-level syntax, mostly for people who'd want to quickly create simple formats and languages based on trees. Or write things down in a way that preserves their tree structure, so they are parseable by a computer later. It's so simple and unobtrusive that you can just type things by hand -- that's a property that very few syntaxes have. That's something I wanted to have and that was not available and is not available today outside of Jevko. This is why I created it. To satisfy my sensibilities and design constraints.

I digress again.

I think I'm gonna stop this here. It's pretty lousy, but it does get the ball rollin' further. I wonder where it'll go.
