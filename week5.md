# Arrays and Algorithms
### Arrays
Arrays are like lists in Python, with some differences. An array is a linear collection of variables with the same type. In other words, arrays are like Python lists, except they can only hold variable of one type and they are fixed in size on creation (ways to create variable sized arrays are discussed in later weeks).

The syntax for arrays are

        int myArray[10]; // Create an integer array of size 10
        char myOtherArray[5]; // Char array of size 5
        myArray[0] = 1; // Arrays are indexed from 0
        printf("%d\n", myArray[0]); // Prints 1

Arrays are not just fixed in size, they need to have a constant size when you compile the code. That means you cannot use a number from input as the size of your array. The compiler needs to specify a constant size for the computer during compilation.

### Arrays are pointers
```myArray``` in the code above is actually a memory location to the first element in the array. This is how C tracks arrays. To find the value of ```myArray[0]```, the computer retrieves the value stored at the location ```myArray```. To retrieve the value of ```myArray[5]```, the computer retrieves the value at ```myArray``` shifted to the end by 5 ```int``` size bytes.

        *myArray; // Same as myArray[0]
        *(myArray + 5) // Same as myArray[5]

### Passing arrays into functions (Don't forget it's buddy)
A function that takes an float array as input may look like this

        float maxNumber(float numbers[]) {...}

Alternatively, because arrays are pointers, the following is equivalent

        float maxNumber(float *numbers) {...}

However, the array by itself is not enough information for the function most of the time. To be able to loop through the array, our function ```max``` needs to know the size of the array, otherwise it can loop forever.

        for (int i = 0; ; i++) {
                if (numbers[i] > max)
                        max = numbers[i];
        }

This doesn't look right. C allows you to index a value outside of the range of your array. However, index too far outside of the range and your program will silently crash.

C does not have a len function to get the length of an array like Python. (Remember that to the computer, an array is just a pointer) So we will also need to pass the size of the array to our function

        float maxNumber(float *numbers, int arraySize) {
                // Smallest float value, defined in <float.h>
                float max = FLT_MIN;
                for (int i = 0; i < arraySize; i++) {
                        if (numbers[i] > max)
                                max = numbers[i];
                }
                return max;
        }

The size number is sometimes called a "buddy variable".

### Big O Notation
Programmers care about the speed of their algorithms, and big O notation is used to compare the speed of different algorithms.

Let's start with an example, what is the value of count?

        int count = 0;
        for (int i=0; i<n; i++) {
                for (int j=0; j<n; j++) {
                        if (array[i] == array[j]) {
                                count++;
                        }
                }
        }

Count will have a value of $n^2$ by the end. The inner loop of the function is executed $n^2$ times. 

Big O notation is a way of describing the speed of an algorithm with relation to the size of it's input. We say the above algorithm has a big O of O($n^2$).

Let's do another example

        int count = 0;
        for (int i=0; i<n; i++) {
                count++;
        }
        for (int i=0; i<n; i++) {
                for (int j=0; j<n; j++) {
                        if (array[i] == array[j]) {
                                count++;
                        }
                }
        }

This is the same algorithm with an additional for loop. The value of count will be $n^2 + n$. But we still say the algorithm has a big O of O($n^2$). Why? This is because for large n, the n^2 component will be much larger than the n component. In other words, $n^2$ dominates $n$. For describing algorithms, we care a lot about how it will scale, so we only describe the terms that matter for large n.

In other words O($n^2 + n$) = O($n^2$), and O($10n^2 + 3n$) = O($n^2$)

The dominance relationship goes
$x!$ >> $2^x$ >> $n^3$ >> $n^2$ >> $nlog(n)$ >> $n$ >> $log(n)$ >> $1$