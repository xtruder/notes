# Bsideslj2017

## 1. Automated binary analisys

Analyzing programs using algoritms

### Intro

- More processing power made this possible
- Darpa grand challenge

### Basic concepts

- Intermediate representations like LLVM, VXR, ...

**CFG Recovery**

Build graph with jumps as edges abd basic blocks as nodes

What about higher order functions, 

**Value-Set analisys**

Approximate program states

**Data-Flow analisys/Tain analisys**

Track data and its dependencies. Detect functions that handle user input.
Granularity In bytes in bits.

**Constraint solving**

Z3 and simliar theorem provers that do SMT solving. Anger
