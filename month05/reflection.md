# September reflection

I have working on contributing to open source projects for a while now, and this month I focused on compiler development. I spent a lot of time understanding the inner workings of the compilers and how they optimize code. I studied different optimization and a lot of material that helped me understand how compilers work. I was also mentored by Omar azizi, who is an expert in compiler development.

this is a bunch of material of what I have learned and studied this month:

- [Getting started with llvm](https://youtu.be/3QQuhL-dSys)
- [An overview of Clang](https://youtu.be/5kkMpJpIGYU)
- [Writing AST matchers for libclang](https://manu343726.github.io/2017-02-11-writing-ast-matchers-for-libclang/)
- [Introduction to the Low-Level Virtual Machine (LLVM)](https://youtu.be/HecW5byOrUY?list=PLDSTpI7ZVmVnvqtebWnnI8YeB8bJoGOyv)
- [How single-iteration InstCombine improves LLVM compile time](https://developers.redhat.com/articles/2023/12/07/how-single-iteration-instcombine-improves-llvm-compile-time#)
- [Scheduling Model in LLVM - Part I](https://myhsu.xyz/llvm-sched-model-1/)
- [The Architecture of Open Source Applications (Volume 1)](https://aosabook.org/en/v1/llvm.html)
- [crafting interpreters](https://craftinginterpreters.com/)
- [LLVM: Canonicalization and target-independence](https://www.npopov.com/2023/04/10/LLVM-Canonicalization-and-target-independence.html)
- [Mapping High Level Constructs to LLVM IR](https://mapping-high-level-constructs-to-llvm-ir.readthedocs.io/en/latest/a-quick-primer/index.html)
- [A Gentle Introduction to LLVM IR](https://mcyoung.xyz/2023/08/01/llvm-ir/)
- [Simple but Powerful Pratt Parsing](https://matklad.github.io/2020/04/13/simple-but-powerful-pratt-parsing.html)

Im currently searching for an issue on the [llvm-project](https://www.github.com/llvm/llvm-project) repository to contribute to. I have been looking for issues that are labeled as "good first issue" or "help wanted". I have also been looking for issues that are related to compiler optimization and linting such as clang-tidy.
the repo is very active so its a bit hard to find an issue that is not already being worked on. but i found this issue [Clang-Tidy #64988](https://github.com/llvm/llvm-project/issues/64988) which  is a couple of years old but still produces a warning that when followed produces code that does not compile.

I also explored the possibilty of writing my own frontend for a programming language. I have been thinking about writing a front end for a language that is similar to C as learning milestone. and also explaored the possibility of adding backend support for a new architecture. a frined told me aboutadding support for the c6000 texas instruments architecture. I have been looking into the documentation and the codebase of the llvm-project to understand how to add support for a new architecture, its either you do and RFC and wait or just fork it.
