---
description: C/C++ notes
---

# C

#### C Source Code File -&gt; Compilation \(Preprocessor -&gt; C Compiler\) -&gt; Object Code \(.o or .obj\) -&gt; Linker \(links all compiled programs into an executable .exe\) -&gt; Loader \(executes the executable file, loads the .exe to the primary memory RAM\)

The preprocessor optimizes the code \(takes out redundancies, commentaries, empty lines\) before actually compiling the code. The object code can be directly the machine code or not, sometimes it is compiled into assembly, then from assembly to machine code or directly. 

#### enum

It's a user defined data type in C. Works like dictionary in Python but relating fixed indexes to variables, it's usually used when defining states for FSM. An example:

`enum week{Mon, Tue, Wed, Thur, Fri};  
int main()  
{  
    // Instantiating enum  
    enum week day;  
    day = Tue;  
    // Is gonna return the number 1  
    printf("%d",day");  
    return 0;  
}`

Note that two enum names can have the same value

#### Variables

* uint8\_t = 8 bits, unsigned integer of length 8.
* float\_t_=_ type of __float that is determined by the value of FLT\_EVAL-METHOD \(which is defined in the compiler\)
* Underscore before variable =
* temp = is a variable that you just use to store some value to do temporary calculations or so, it seems that it can be used multiple times in a row? 

Header Files: Using header files is a GOOD practice to do. Just used in the compiling proccess in order to the compiler to know which functions are exported by a module, after this process the header files are not needed anymore. Header files really come into picture when we're using a module that we developed on another project, because then we can just include our header file to use the functions we declared.

[https://dev.to/narasimha1997/understanding-c-c-build-system-by-building-a-simple-project-part-1-4fff](https://dev.to/narasimha1997/understanding-c-c-build-system-by-building-a-simple-project-part-1-4fff)

