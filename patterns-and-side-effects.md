    a != 5
    b != $a + 1  ## Do we need a notation for "current value of"? Why do I like this?

Or should side-effects versus bind-a-new-name be a feature of patterns? And LHSes are all patterns? If that's the case, we need space in the syntax for the modes. In fact, any valid expression (RHS) would be a valid pattern (LHS) (it would be a test, I suppose!), but LHSes can also introduce mutable/immutable variables, as well as assign to existing mutable variables. Is that all? Three things seems weird...

Well, not any valid RHS. Constructors (whatever they are) are okay in patterns, but not function calls. However, function call syntax doesn't seem like a good thing to steal. And punctuation is so precious! /precious.../ Well, mathematical operators aren't constructors:

    (*a /b +c) <- the_tuple ## I have no idea which is which!
    (a! =b =c!) <- the_tuple ## `!` for side-effects, `=` for initialization
    (a! 'b' 'c'!) <- the_tuple
    (a! *b *c!) <- the_tuple
    (!a b:nat !c:string) <- the_tuple ## I just remembered that this might be a typed language...
    (a! *b *c! d~) <- the_tuple ## with parameters, we can bring it up to an even four
    
Another problem is that patterns should be extensible, and not just with constructors (or, we need "constructor" to refer to something broad). Regexpes in patterns! Custom regexp syntax in patterns! Wacky sequence stuff (like Redex's "magic squared"?)!

    "Name: [name:string] Age: [age:string]" <- read_line
    /[*name]\s*[*age]/ <- please_ignore_my_perversion_of_regexp_syntax

Pattern matching can fail. One person's "can't happen" is another person's control flow.

Also, we sometimes wish to apply functions in the middle of pattern-matching. But backwards, since the input is anonymous and the output is named. Also, the functions pretty much have to only take one argument, but multiple return values is totally coherent, provided there is syntax for it. This is sort of a rabbit hole. It's useful to have this feature in extensible old Racket `match`, but one wonders whether this is some sort of attempt to move all computation to the LHS.

    "Age: [(age:int)esrap]" <- read_line ## Gotta get that out of my system
    "Age: [age:int <- parse(_)]" <- read_line ## Cute! Orthagonal! Ish! Assuming `_` is a convenient quick lambda syntax! And lambdas can have blocks for bodies!

(Riffing backwards on that last one, what if we made it so that a lone LHS (like `age:int`) were a valid statement? What would the implications of that be? Feel free to discuss the idea in any way that appeals to you.)
