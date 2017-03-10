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

Works with sso, so we can log in to any other apps, that integrate facebook, twitter, google
as login methods.

## 4. ROP, CFI, RAP, XNR, CPI WTF?

- one off memory overflow
- use after free

When we have control over code pointer(return address, vtable, ...)

- Code injection
- Core reuse attacks (ROP)

### ASLR

randomizes memory loading addresses

**Problems**

- Low entropy on non 64 bit systems
- Constant mappings
- Sloppy ASLR
- No randomize on fork

Randomize more things, reorder functions

- Address space layout randomizations

Still not enough entropy?

- Permutate basic blocks

WUT, still not enough?

- Randomize general purpouse register usage

#### JIT ROP

Just in time rop, using memory leaks.

#### Blind ROP

Brute force until you find a gadget and look for results (does it crash, what hapens with stack)

**Assumptions**

- Unlimited trues
- No re-randomization
- Need to know rough code location

#### Leaking code pointers

### Mitiagete code infoleak

- Multivariate execution
- Prevent/mitigate code disclosure
  - Execute-no-read XnR
  - Destructuve code reads (if you are reading a code, you are destructing it)
  - No execution after read (NEAR) - Same things, using hardware features
- Hide code pointers and pointers to code pointers
- Re-randomize every N ms (Shuffler) - performance issues of course
- Execution path randomization - You decide on every code block and choose one

### Deterministic protections

#### Code flow integirty

- Enforce that control-from transfer are withing control flow graph
- Static control-flow graph = security policy

Forward-edge CFI
Backward-edge CFI

This does not work well in practice

#### Coarse-grained CFI policies

- return address must be preceded by call
- Inderect calls only to
  - function beginning
  - adress token functions
- Type- based policies for inderect calls

  Pax RAP
  
  Can only call functions with some signature
  
#### Attacks on CFI

Static CFI can be broken:

- Control-Flow bending
- There anre many helper functions that are called from everywhere

#### Code pointer protection

- Certain code pointers(stack pointers, RELRO)
- Protecting return addresses
  - Shadowstack (windows)
  - Splistack (LLVM safestack)
  - Obfuscation (PaX RAP)
  
#### Data-Only Attacks

- Data-oriented programming DOP is turring complete
- CFI is broken only data only attacks

### Data-Flow integrity

- Check whether variables being read are the ones that are allowed

### Conclusion

- Security vs perfmance
- All these protections make attacks a lot more difficult

CFI safestack llvm
