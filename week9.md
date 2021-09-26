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

We use the ```malloc``` and ```free``` function from the ```stdlib.h``` library

        #include <stdlib.h>
        #include <stdio.h>

        ...
        printf("Array size: \n");
        scanf("%d", &array_size);
        double *array = (double *) malloc(sizeof(double) * array_size);
        
