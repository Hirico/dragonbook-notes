
# 1.1 Language Processors 

### Example 1.1
* > In order to achieve faster processing of inputs to outputs, **some Java compilers,
called just-in-time compilers**, translate the bytecodes into machine language
immediately before they run the intermediate program to process the input.  -- page 1

    首先，在Java中，注意**区别**把源代码编译成字节码的bytecode compiler和这里的just-in-time compiler，它们是独立的两个组件。在讨论Java上编译的概念时，一般把它们看成独立分开的、包含完整行为的**两个compiler**，而不是把它们放到一个大的analysis-synthesis model里*。

    Java的just-in-time compiler (JIT compiler) 是包含在JVM中的，因此是否使用JIT compiler、JIT compiler的版本和具体行为都是因JVM而异的。
    
    以当前主流的Oracle家的HotSpot（也就是OpenJDK的JVM）为例。HotSpot会把检测到经常被调用的代码交给JIT compiler编译后执行，而其它代码则不走JIT compiler，直接在字节码的层次上靠解释器执行。

    **JIT**本身是一个**无关具体语言**的概念。例如现在Chrome用的JavaScript引擎V8、一种C++的解释器[Cling](https://root.cern.ch/cling)都用到了JIT。

    资料：[Java JIT](http://javajee.com/just-in-time-jit-compiler-versions-client-server-and-tiered-jvms) 
    | [JavaScript JIT](https://hacks.mozilla.org/2017/02/a-crash-course-in-just-in-time-jit-compilers/)
    
    *存在把Java code编译到native code的compiler，见[GCJ](https://en.wikipedia.org/wiki/GNU_Compiler_for_Java)



# 1.2 The Structure of a Compiler 

### 1.2.8 The Grouping of Phases into Passes
* >  In an implementation, activities from several phases may be grouped together
into a pass that reads an input file and writes an output file.

    按照此处pass的定义，Java bytecode compiler是one-pass的，[编译过程在内存中完成，直接将源文件生成class文件](http://openjdk.java.net/groups/compiler/doc/compilation-overview/)。但是这并不是[wikipedia上pass的定义](https://en.wikipedia.org/wiki/One-pass_compiler)，这个问题在stackoverflow上就产生过[争论](https://stackoverflow.com/questions/35673818/difference-between-one-pass-and-multi-pass-compilers)。

