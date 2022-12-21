# Whitespace

// stream of consciousness

what is whitespace?

well, it is not an easy question to answer, certainly not an easy one -- you, one might think that it is easy, but it turns out not to be 

not as straightforward as one might think; it's not straight

is it these characters: ' ' \t \n \r \v -- did I forget one (I'm not looking, doing this from memory)? anyway, ASCII characters that qualify as space below and including 32?

well that's the ASCII definition of it, something like the ascii definition of it

but now we have Unicode, so that's not enough; the ASCII whitespace is only a subset of Unicode whitespace

now which UTF characters unicode that is should qualify as whitespace? only the ones that have some flag set? how do you keep track of this flag? has it all become a mess or is it just me? likely just me

anyway if you are to standardize something like the trim aka strip function/method for strings in a programming language it would be nice if it was clear what exactly it strips or trims -- is it just the ASCII whitespace or is it unicode whitespace as well -- does it get it all, does it have its own definition perhaps?

maybe it's configurable? but why should I have to care? what's the default?

this is why it's not that easy to decide on a standard and thus explain whitespace handling and explain whitespace and implement things that deal with it -- you start talking about whitespace ; the minute you do that you drag in this immense complexity

now add to that kinds of whitespace -- particularly newlines

every operating system (exaggerating) has its own !@#$%^ idea of what constitutes a linebreak -- it would be easy enough if they would all use a single character, just disagreed on which is it or even all used two characters, just disagreed which; but no, some use one, some use two, and subsets are involved here

now go and make some routine dependent on linebreaks -- you are going to have a bad time; oh and unicode, that's another thing, it throws in a few more line break characters

that makes me think of dates and times and calendars and dealing with them -- well actually whitespace is a piece of cake compared to that mess
