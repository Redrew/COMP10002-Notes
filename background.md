# Background to the Subject
Looking back at the course, I have realized that COMP10001 glosses over a lot questions. These are questions like:
Why do we need a compiler?

# From the bottom up
The CPU is a calculator that executes instructions from memory. These instructions are encoded as bits, and they can tell the CPU to perform arithmetic, write data to memory, and jump to other instructions.

Coding in the bits language is hard. So programmers wrote assembler programs that transform human readable instructions into binary. These instruction languages are called assembly languages. They are designed specific to the hardware's accepted instructions, so assembly code on my computer may not work on yours.

Sharing code when everyone is using different languages is impossible, so programmers again wrote programs to transform standard languages down to assembly. These programs are called compilers. C was one of the first "portable" languages, and it was designed to help write the Unix operating system. 
