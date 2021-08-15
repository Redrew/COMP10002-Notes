# Functions and Memory Addresses

### Functions
Functions allows programmers to reuse code. Separating code into functions often leads to less repetition, and more readable code!

Much like variables, we need to tell the compiler the 'type' of our function. In C, this means specifying the type of the returned value and the types of the function's arguments.

        [return value type] function_name([type] arg1, [type] arg2) {
                ...
        }

A function that you are familar with is the main function

        int main(int argc, char *argv[]) {
                return 0;
        }

From the definition, we know that the main function returns an integer, and takes two arguments: an integer argc, and argv (argv's type is more complicated and will be explained shortly).

If your function doesn't return a value, declare your function with the ```void``` type

        void print_number(int n) {
                printf("%d\n", n);
        }

### Memory
Here comes the most important concept for a C programmer, the memory stack. Computers memory is essentially a huge table for storing data. This table stores data in bytes and each byte is labelled 0, 1, 2... This label is also called an address or a pointer.

| Address/Pointer     | Data        |
| ----------- | ----------- |
| 0           | 255         |
| 1           | 0           |
| 2           | 0           |
| 3           | 11          |
| ...         | ...         |

#### Memory Operators
You can get the address of a variable in your program with the ```&``` operator.

You can use it to print out the address of a local variable.

        int num = 0;
        printf("%p\n", &num);

Note: ```%p``` is the format specifier for an address (pointer).

A pointer to a variable of ```[type]``` has the type of ```[type]*```. We can store the pointer to num with

        int num = 0;
        int *num_pointer = &num;

You can get the value at a pointer / change the value at a pointer using the ```*``` operator.

        int num;
        int *num_pointer = &num;
        *num_pointer = 0; // num = 0
        int other = *num_pointer; // int other = num;

#### Hexadecimals
On my computer, printing the pointer of ```num``` gave me ```0x7ffbffffa93c```. This is a number in hexadecimal form. Hexadecimal numbers have 16 symbols (0123456789abcdef) instead of 10. This allows us to represent large numbers in less symbols. Because computer addresses can get very large, they are usually printed in hexadecimal form.

#### Stack
A C program stores local variables in memory consecutively. This section of memory is referred to as "the stack".

        int a = 0;
        int b = 0;
        printf("%p %p\n", &a, &b);
The above code gave me ```0x7ffbffffa960``` and ```0x7ffbffffa964```. The value of the pointers will change every time I run the program because the next available address on the stack will change depending on the other programs running on my computer. What will not change is the relative difference between the pointers. ```int``` variables have a size of 4 bytes on my computer. Because local variables are assigned memory consecutively, a and b are next to each other in memory.


| Address/Pointer     | Data        |
| ----------- | ----------- |
| ...         | ...         |
| 0x7ffbffffa960 | 0           | 
| 0x7ffbffffa961 | 0           | 
| 0x7ffbffffa962 | 0           | 
| 0x7ffbffffa963 | 0           | 

### Pointers and Functions
A C program copies the value of variables passed into a function. This means that the address of the variable you pass in to a function will be different to the address of the variable in the function.

        void print_address(int n) {
                printf("%p\n", &n);
        }

        int main(int argc, char *argv[]) {
                int num = 0
                printf("%p\n", &num);
                print_address(num);
        }

The above code will print two different addresses. This means that any changes to the argument's value inside a function will not change variables outside of the function.

#### Variable scope
Local variable - a variable that can only be accessed inside of the function, it's value is 'destroyed' after the function ends. ```int a = 0;```

Static variable - a variable that can only be accessed inside the function, but it's value persists between function calls. ```static int a = 0;```

Global variable - a variable that can accessed by every function, defined outside of a function. ```int a = 0;```

#### Changing variables in function
What can you do if you want your function to change the value of a variable outside the function? You can pass the address of that variable as an argument instead.

        void add_one(int *n_pointer) {
                *pointer = *pointer + 1;
        }
        int main(int argc, char *argv[]) {
                int num = 0;
                add_one(&num);
                printf("%d\n", num);
        }
