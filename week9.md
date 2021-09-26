# Time to have some fun

### Structs
Structs are a collection of different data. Unlike arrays, structs can contain different data types.
We do need to specify example what data types are in a struct.

        struct Book {
                char *title;
                char *author;
                int year;
                int pages;
                float price;
                int checkedout;
        };
        struct Trilogy {
                struct Book books[3];
                char *name;
        };

        int main(...) {
                struct Trilogy trilogy;
                trilogy.name = "Foundation Series";
                trilogy.books[0].title = "Foundation";
                trilogy.books[0].author = "Isaac Asimov";
                trilogy.books[1].title = "Foundation and Empire";
                trilogy.books[1].author = "Isaac Asimov";
                trilogy.books[2].title = "Second Foundation";
                trilogy.books[2].author = "Isaac Asimov";
        }

Somethings we can takeaway from the example above.
* Structs can contain arrays, but we have to specify their size (compiler needs to know the size of each struct).
* Member/attribute of a struct can be accessed with dot: ```struct_var.member```
* struct variables are created with ```struct struct_name variable_name```
* structs can contain structs. In fact, they can contain a pointer to the same struct type (we will get to this later)

#### Defining types

        struct Book {
                ...
        };
        typedef struct {
                ...
        } book_t;

        struct Book book1;
        book_t book2; // Same, but simpler

It is much easier to create struct variables if you create a type for that struct. It is good practice to define structs with typedef.

#### Structs in arguments

        book_t checkout(book_t book) {
                book.checkedout = TRUE;
                return book;
        }

        ...

        book = checkout(book);

Structs are very similar to primative data types. They are copied when passed into a function and they can be returned from a function.

Sometimes we want to alter a struct inside a function, in that case, we need to pass a pointer of the struct into the function.

Note: It is preferred to pass struct pointers rather than the variable at all times. This is because it is time and memory intensive to copy structs when they are big.

        void checkout(book_t *book) {
                (*book).checkedout = TRUE;
                book->checkedout = TRUE; // Same, but simpler
        }
        ...

        checkout(&book);

When dealing with struct pointers, ```->``` is a useful operator to access struct members.

#### Comparing structs
Structs cannot be compared by default. This is because there is no logical way to compare a custom data collection without more help from the programmer.

This is why we define comparison functions for structs.

        /* We decide to compare books first by the title
           then the author */
        int cmp_book(book_t *book1, book_t *book2) {
                int name_dif = strcmp(book1->title, book2->title);
                int author_dif = strcmp(book1->title, book2->title);
                if (name_dif != 0) {
                        return name_dif;
                } else {
                        return author_dif;
                }
        }

Comparison functions are helpful when you are sorting structs.

### Dynamic Memory
We finally learn how to create variable sized arrays and data that can be returned from a function as a pointer without being destroyed.

We do this with the ```malloc``` and ```free``` function from the ```stdlib.h``` library. malloc and free works with
the operating system's memory management system to create persistent memory. This memory will stay until it is freed with free.

        #include <stdlib.h>
        #include <stdio.h>

        ...
        printf("Array size: \n");
        scanf("%d", &array_size);
        double *array = (double *) malloc(sizeof(double) * array_size);

        // Check we got allocated memory
        if (array == NULL) {
                printf("Not enough memory\n");
                exit(1);
        }
        
        // Do things with array
        ...

        // Release memory
        free(array);
        array = NULL;

Somethings we can takeaway from the example above.
* malloc is a generic function. It takes as argument the number of bytes to be allocated, and it returns a pointer with type (void *)
* It is up to the programmer to then assign a type to the pointer by casting ```(new_type *)``` the return value.
* sizeof returns the byte size of primitive data types. Always use sizeof instead of hardcoding the sizes of primitives, because it can change from machine to machine
* It is good practice to always check that malloc returns a valid address. malloc can fail if the computer is out of memory, in which case it will return a NULL pointer (which has a value of 0)
* NULL has value of 0, default return value if malloc cannot allocate that much memory
* Always free memory after you are done. Future assignments will check that all memory is freed after your program finishes, memory leaks are a problem in long programs/loops
* Rule of thumb: always have one ```free``` for every ```malloc```
* Set pointers to NULL after they are freed because they no longer point to valid memory

#### Resizing arrays
What if we need to resize our allocated memory? We can do this with ```realloc```. realloc creates a new section of memory with the new size and copies all data from the old memory block, then it frees the old memory.
realloc

        ...
        double *array = (double *) malloc(sizeof(double) * array_size);
        ...
        array = realloc(array, new_array_size);
        if (array == NULL) {
                printf("Not enough memory\n");
                exit(1);
        }

        free(array);
