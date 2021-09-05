# Strings and 2D Arrays

### Even more about Strings
We know that a string is an array of characters. But how do we know when the string ends? C does not track array sizes by default, and the length of the string may not be the size of the array itself. (eg. if you store "Hello" in an array of size 500)

The end of a string is indicated by the null character ```'\0'```. The string "Hello" would be stored as

```'H' | 'e' | 'l' | 'l' | 'o' | '\0'```

In general, a string with n characters need to be stored in an array of size n+1 (because we need to terminate it with the null character).

```'\0'``` has an integer value of 0

### Read only string
The following statements are different in C

        char *str1 = "Hello World";
        char str2[] = "Hello World";

This is non intuitive because arrays are represented as a pointer to the first element. Both ```str``` variables point to a character array of length 12 containing the characters ```Hello World\0```. However, the first array is a string literal and it's contents are read-only, while the second array's contents can be changed.

```str1[0] = 'h'``` would give an error

```str2[0] = 'h'``` works perfectly fine

This is to do with how C compilers treat string literals ```"..."```. Whenever you write string literals, the compiler stores the string in a read-only data memory section. Compare this with when you create an array like ```char str3[10]```, the array is stored in the stack, and can be edited. ```char str2[] = "Hello World";``` is a short hand for

        char str2[12] = {'H', 'e', 'l', 'l', 'o', '\0'};

### Arguments
```char *argv[]``` in the main function is an array of string literals. C uses argc and argv of the main function to pass arguments to the program.

You would be familiar with program arguments from using gcc. For example when we run the command ```gcc -o my_program my_program.c```, we are calling the program ```gcc``` with 3 arguments, ```-o```, ```my_program```, ```my_program.c```. C actually considers the program name as an argument, so the main function is called with 

        argc = 4
        argv = ["gcc", "-o", "my_program", "my_program.c"]

Note that argc is needed so we can loop through the arguments, otherwise we cannot do this

        for (int i=0; i<argc; i++) {
                printf("%s\n", argv[i]);
        }

### 2D arrays
Creating multidimensional arrays is easy in C, if you know the sizes of each dimension.

        int matrix[10][10]; // 10 by 10
        int tensor[10][10][10]; //10 by 10 by 10

### Defining types
Writing the same type signature for a variable like a multidimensional array is tiring. An elegant solution is to define a special type.

        typedef int [10][10] matrix_t;
        typedef int [10][10][10] tensor_t;

        matrix_t my_matrix;
        matrix_t my_other_matrix;
        tensor_t my_tensor;

