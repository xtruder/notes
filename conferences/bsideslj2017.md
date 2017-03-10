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

**Agumented execution**

Symobilic execution with help of fuzzing

### Tools

- Angr (python)
- Bitlaze
- Z3
- Sage

### Angr

- Symoblic exection
- Calling functions from python
- Reverse engineering
- Function inversion
- Bypasses anti-debugging techinques

## 2. Peculiar SSH

Example usage:

```
tar xf - ./files | xz | pv | ssh -o "Compression no" box "cat > file.tar.xz"
```

### Two-Factor Authentication

- Google authenticator (package in nixos: https://github.com/NixOS/nixpkgs/blob/master/pkgs/os-specific/linux/google-authenticator/default.nix)
