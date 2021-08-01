# The Journey Begins


### A basic C program

        int main(int argc, char *argv[]) {
                return 0;
        }

Every C program has a main function like above. All function calls are made inside the main function (or as a result of some function that main calls).

When we run a C program, the computer will look for a function called main, and pass in two parameters... (argc and argv, more on that in a later week)

### Types
The ```int``` and ```char``` in the code above are types. All variables have a type associated with it that defines what kind of data it is. The type lets the computer know how much memory is needed to store the data and how to interpret it.

Each variable's type must be declared before we can store or read value from it. This is a declaration.

        int num;

After the declaration we can initialise the variable with a value and perform operations on it.

        int num;
        num = 1;
        num = num + 2;

**Warning:** Initialization is important because there is no default value for variables in C. The computer can allocate memory that has values left from before, so an uninitialised variable's value may be entirely random.

Declaration and initialisation can be combined.

        int num = 1;

Basic types in C:
        
```int = 3``` - integer (whole number)

```float = 3.14``` - real number

```double = 3.143141592653589793``` - real number (a double can represent real numbers with more precision than a float because it has double the memory size of float)

```char = 'c'``` - a character (ASCII)


### Hello World

        #include <stdio.h>
        int main(int argc, char *argv[]) {
                printf("Hello World\n");
                return 0;
        }

We need to import the standard input & output library (stdio) to write our hello world program. Strings are surrounded by double quotation marks ```"``` as opposed to single quotations ```'``` for characters. Printf does not print newlines by default, so you will usually need to include ```\n``` at the end of your string.

### Input and Output
Printing just static texts is not fun. C's printf can print numbers with some formating magic.

        printf("This is a number: %d\n", 3);
        printf("This is a double: %lf\n", 3.14);
        printf("This is a double with 1 decimal place: %.1lf\n", 3.14);

We can also read in input with scanf.

        double placeholder;
        printf("Give me a double: ");
        scanf("%lf", &placeholder);
        printf("You gave me: %.1lf\n", placeholder);

```%lf``` tells scanf to expect a real number in the input. It stores the value into the double variable placeholder. ```&``` is a special operator in C, ```&placeholder``` evaluates to the memory location of placeholder, which scanf uses to place the value in the correct location. We will learn more about the ```&``` operator in later weeks.
