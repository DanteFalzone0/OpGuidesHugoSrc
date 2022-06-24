## Would you like to speak to an Operator?

+,-,/,*,%,>>,<<,^,|,&,&&,||,==,>,<,<=,>=

## Going with the flow

if/elif/else, for, while, brief note on recussion, goto

example of to small of an int on a loop

## Getting Functional

In most programming languages, we have the concept of **Functions**. Functions let us break up code into digestable sections and reuse things. When we call `print()` we're actually using a function that's built in... [TODO]

fns, the stack

### The Stack

[TODO stack plates visual]

When we call a function, we store the current state of the calling function, move to the address of the called function, do the thing, then return to the original (calling) function and restore this state. This gets complicated when we start wanting to call a function from in a function from in a function .... you get the idea. Basically, we need a place to store the return address (among other state) to know where we want to go back to when the called function returns, but we can't just put these all in CPU registers since we only have so many CPU registers.

One option would be to give every function a place in RAM. This won't work for a varitey of reasons, one is because it uses a ton of space by not letting us reuse space between functions, and we want local variables to only be valid for that call of the function anyway (This is one reason why we have `static`, if you do need state to be preserved). Another is that we want to be able to call our functions from multiple places (it would be awful if we had to store a ton of coppies of every function in RAM!) So, we let functions return and then reuse their space.

So, we instead want to make a place to store the return address of each function (and their variables) as they're called. We do this with a **Stack**, in this case, *The* Stack. If someone says *The Stack* this is the stack they mean. So, uhh, what's a stack?

* Each function call adds its own section to the stack
* Each stack section contains two types of data:
  * the RA from the caller
  * The local variables used by the the currently executing function
  * Arguemnts to the function
* When the function returns it's section is reoved from the stack
* This keeps the amount of memory on the stack at a minimum
  * Total memory usage across all functions can be greater than RAM size
  * Limit is now the memory usage of functions at deepest call hierarchies
    * **Stack Overflows!**
    * Really hard to anticipate calculate
      * Super annoying with recursion, hence why it's often avoided.
* So, we maintain a stack pointer, this is an *offset*, so each function's variables are looked up by a base + offset. The base is th estack pointer, the offset is the particular variable we want to access.

 So, we use a stack! - LIFO (not FIFO) - we only operate on the top of the stack

[TODO] what's a stack