# Compiler Notes ˆˆ

So I'm dumping all my notes here from this Stanford compiler course I'm taking (https://online.stanford.edu/courses/soe-ycscs1-compilers). This is basically my brain on paper and might be a bit chaotic but that's how I learn fast ˆˆ

Will keep adding my notes as I go deeper into the course. Feel free to learn along with me or point out if something doesn't make sense!


## Day one

Key Points:
- Prof explaining 2 ways to run programs: interpreters vs compilers

Interpreters:
- Takes program + data → direct output  
- Runs stuff immediately, no preprocessing
- Downside: Way slower (like 10-20x slower)

Compilers:
- Takes just the program → makes executable
- Can run executable many times w/ different data
- Offline process (preprocesses first)

Cool History:
- 1950s: IBM 704 showed software costs > hardware costs (big deal back then)
- Speed coding (1953):
  * First interpreter by John Backus
  * Made programming faster but programs ran slower
  * Used 30% of computer memory (yikes)

FORTRAN:
- Backus's next big thing (1954-57)
- First successful high-level language
- Took 3 years instead of 1 (classic software project lol)
- By 1958: 50% of all code = FORTRAN (insane adoption rate!)

Modern Compiler Structure (same as FORTRAN 1!):
1. Lexical analysis & parsing (syntax stuff)
2. Semantic analysis (types, scope rules)
3. Optimization (make code faster/smaller)
4. Code generation (translate to machine code/bytecode)
