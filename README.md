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

\`\`

