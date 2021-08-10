# Finally Loops!

### If Else
        if (number % 2 == 0) {
                printf("Fizz\n");
        } else if (number % 3 == 0) {
                printf("Buzz\n");
        } else {
                printf("Boo\n");
        }

If else statements in C are very similar to Python. However, in C, if else statements must surround the condition with ```(...)```, and ```else if``` is used instead of ```elif```. The execution block inside an if statement must be surrounded by ```{}```. This is because C doesn't not read indentations like Python.

You can skip ```{}``` in one case - if your execution block is only one line. Such as

        if (number % 2 == 0)
                printf("Fizz\n");
        else if (number % 3 == 0)
                printf("Buzz\n");
        else
                printf("Boo\n");

If you write

        if (number % 2 == 0)
                printf("Fizz\n");
                printf("Buzz\n");

Then the third line will be executed regardless of the conditional.

### Operators
#### Logical operators

        && - and
        || - or

#### Incrementing operators

```int a = 0;```

```a++;``` after operation, a evaluates to 1, the expression itself evaluates to 0

```++a;``` after operation, a evaluates to 1, but the expression itself evaluates to 1!

```a--;```

```--a;```

### While Loop

        int counter = 0;
        while (counter < 10) {
                printf("%d\n", counter);
                counter++;
        }
### For Loop

        for (int counter = 0; counter < 10; counter++) {
                printf("%d\n", counter);
        }

The equivalent loop!
### Switch

        switch (number) {
                case 3:
                        printf("Value is 3\n");
                        break;
                case 7:
                        printf("Value is 7\n");
                        break;
                default:
                        printf("Value is not 3 or 7\n)
                        break;
        }

Everything you can do with a switch can be accomplished by a series of if else statements. Try to avoid switch statements.

### Define
It is not good convention to leave "magic numbers" (any number other than 0 or 1) or non self-explanatory values in your code.

That's where constants come in. Because we cannot declare a true constant value, we have to use the compiler directive ```#define```

        #define MY_CONSTANT 123

You may notice that ```#define``` is similar to ```#include```, both are instructions to the compiler. The latter tells the compiler to include certain libraries in compiled program. The define statement above tells the compiler to replace all instances of phrase ```MY_CONSTANT``` with ```123``` before compiling the code. So during compilation, the line ```printf("%d\n", MY_CONSTANT);``` is replaced with ```printf("%d\n", 123);```


### A bit more about types
#### ```int```
Unlike Python, ```int``` in C is limited in the range of numbers it can represent because it has a fixed size (4 or 2 bytes, depending on your machine). ```int``` is bounded to [$-2 ^ {31}$, $2 ^ {31} - 1$], which is equal to [-2147483648, 2147483647]. 

Attempting to add above the limit will cause overflow ```2147483647 + 1 = -2147483648``` and ```-2147483648 - 1 = 2147483647```. This is certainly a counterintuitve behaviour, so be careful your int numbers do not exceed the limits.

#### ```bool```
There is not a ```Boolean``` type, instead logical expressions are evaluated as int. Therefore, there are no Boolean constants like ```True``` or ```False```.

0 - False

Not 0 - True

If you want to write an infinite loop you can write

        while (1) {
                ...
        }

Or even better you can define a true constant

        #define true 1

        while (true) {
                ...
        }

And one step beyond if your compiler supports the C standard C99

        #include <stdbool.h>
        while (true) {
                ...
        }

### Input output

scanf returns the number of fields successfully read. Returns the ```EOF``` constant (usually -1) if the end of input is read. End of input can be the end of a file or when the user entered <Ctrl + D> in the command line.

getchar returns the next character read from standard input (stdin), returns the ```EOF``` if the end of input is read. Note that getchar actually returns an int, but for valid inputs you can treat it as a character because positive integers can be cast to ```char```.