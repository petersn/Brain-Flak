# Brain-Flak

Brain-Flak is an "Turing-tarpit", e.g. a language which can, *in theory* compute anything, but in reality is very inconvenient and painful to use. It was heavily inspired by [Brainf**k](https://esolangs.org/wiki/Brainfuck), the original turing-tarpit.

#Tutorial

Brain-Flak has two stacks, known as 'left' and 'right'. The active stack starts at left. If an empty stack is popped, it will return 0. That's it. No other variables. When the program starts, each command line argument is pushed on to the active stack.

The only valid characters in a Brain-Flak program are `()[]{}<>`, and they must always be balanced. There are two types of functions: *Nilads* and *Monads*. A *nilad* is a function that takes 0 arguments. Here are all of the nilads:

 - `()` +1.
 - `[]` -1.
 - `{}` Pop the active stack.
 - `<>` Toggle the active stack.

These are concatenated together when they are evaluated. So if we had a '3' on top of the active stack, this snippet:

    ()(){}
  
would evaluate to `1 + 1 + active.pop()` which would evaluate to 5. `<>` evaluates to 0.

The monads take one argument, a chunk of Brain-Flak code. Here are all of the monads:

 - `(n)` Push 'n' on the active stack.
 - `[n]` Print 'n'.
 - `{foo}` While active.peek() != 0, do foo.
 - `<foo>` Execute foo, but evaluate it as 0.

These functions will also return the value inside of them, so

    (()()())

Will push 3 and

    [()()()]

Will print 3 but

    [(()()())]

Will print **and** push 3.

When the program is done executing, each value left on the active stack is printed, with a newline between. Values on the other stack are ignored.

That's it. That's the whole language. 

#Sample code

Here are some full programs that do interesting things.

Adding two numbers:

    ({}{})

Subtracting two numbers:

    {({}[]<({}[])>)}{}

Multiplying two numbers (Positive only):

    (<>)<>({}<>)<>{({}[])<>(({}))<>}{}<>{}({{}}{}<>)

Multiplying two numbers (Any):

    (({})){{}(<>)<>(({}))(()){{}({}[]<({}()<(({}<>)<>)>)>)(({}<(({}))>))({}<({}<({}<>)<>>)<>({}<>)>)({}<(({})){{}{}(())(<><>)}{}>)(({})){{}{}(())(<><>)}{}({}{}[])}{}<>({{}})<>{{}<>{({}[]<([])>)}{}({{}})(<>)}{}{}{}(<>{}<{}><>)({}(<><>))(<><>)}{}({}<{}>)

Modulo two numbers:

    (<>)<>(({})){({}[])<>(())<>}{}({}<(({})){({}[])(<>)<>}{}>)(()){({}<(({})){({}[])<>{}<>}{}>)<>{<>({}[])(<>)}<>}({}<({}<{}>)>)<>{}{({}<>)({}{})<>}{}<>(({}<(({}))>))({}<({}<>)<>({}<><({}<>)>)>){({}[]<({}[])>)}{}(({})){{}{}(<><>)({}<({}<(())>)>)}{}({}<{}{}>)<>{}<>


Print the first *N* Fibonacci numbers:

    <>((()))<>{({}[])<>({}<>)<>(({})<>({}<>))<>}<>{}{}
