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
- SSH ProxtJump in new SSH, similar as ProxyCommand
- Multiple host keys in `/etc/ssh/`

## 3. CookieMonstruo

About hacking social passwords

### Intro

- 2FA makes hacking loging harder
- What about cookie stealing

### FF, Chromium

Stored in sqlite file on filesystem

- Firefox: Stored in plaintext
- Chromium: encrypted, in windows there are functions to decrypt

No tool for chromium decrypt on windows, created a metasplit script called cookiemonstruo
for extracting cookies from browser.

It worked on facebook, which is LOL, because he was running this on totaly different machine.

### Possible issue

- No active session: wait and steal
- User logouts: remove the cookie from victim database

CookieMonstruo has support for both

### SSO
