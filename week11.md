# Numbers Representation and Files
Data is represented as 1 and 0 in computers. This is done with transistor devices that can maintain a constant state of 1 (positive voltage) and 0 (no voltage). We can represent numbers with 1s and 0s by using the binary number system.

Binary numbers (base 2) are very similar to decimals (base 10)

Decimals (base 10): 3089 = 3 * 1000 + 0 * 100 + 8 * 10 + 9 * 1
Binary (base 2): 1011 = 1 * 2^3 + 0 * 2^2 + 1 * 2^1 + 1 * 2^0

Note that n^0 = 1 for any n.

#### Binary addition
1001 + 0011 = 1100

* xxx1 + xxx1 = xx10 (carry the one)
* xx0x + xx1x + 1x = x10x
* x0xx + x0xx + 1xx = x1xx
* 1xxx + 0xxx = 1xxx
* Together: 1110

### Twos Complement
How do we represent negative numbers? One method is to dedicate a bit at the start of the number to indicate the sign of the number (0 - positive, 1 - negative). 

But using a sign bit has two problems:
* There are two representations of zero e.g. 1000 and 0000 (for a 4 bit number)
* It is more complicated to add numbers with different signs e.g. 1001 + 0010 = ?

Twos complement is commonly used to address these two problems. For a number with width w, the first bit has a value of -2^(w-1)

For a 4 bit number:
* 1000 = -2^3 = -8
* 0001 = 1 (all other bits are treated normally)
* 1001 = -2^3 + 1 = -7
* 1111 = -2^3 + 4 + 2 + 1 = -1
* 0000 = 0

There is only one representation of zero: 0000, and we can add negative and positive numbers using normal binary addition.

1001 (-7) + 0010 (2) = 1011 (-5)

<!-- ### Floating point numbers
TBW -->

### Files
File handling in C revolves around the FILE struct defined by stdio.h

You can open a file using
```FILE *file_ptr = fopen("./filename.txt", mode);```

The mode parameter determines what can be done to the opened file
* ```"r"``` - file is read-only
* ```"w"``` - file is write-only, starts writing at the start of file. If the file does not exist, a new file is created
* ```"a"``` - same as ```"w"```, except if the file exists, the program will append content to the end of the file

* ```"r+"``` - opens a file for reading and writing
* ```"w+"```, ```"a+"``` - refer to resources online

To close a file, use
```fclose(file_ptr);```

Always close files at the end of your program.

Reading and writing text to a file is very similar to functions for stdin/stdout

        char c = fgetc(file_ptr);
        fputc(c, file_ptr);
        fprintf(file_ptr, "%d...", num, ...);
        fscanf(file_ptr, "%d...", &num, ...);

Sometimes we want to read and write binary directly. This is useful if the file is not a text file (e.g. executables, object files, data files, video files...)

In that case use

        size_t fread(void *ptr, size_t size_of_elements, size_t number_of_elements, FILE *a_file);
        size_t fwrite(const void *ptr, size_t size_of_elements, size_t number_of_elements, FILE *a_file);

Note that fread and fwrite can be used to write arrays.