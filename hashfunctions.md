# Hash functions

## About

- Hash functions are auxiliary functions

## Usage

- signature (sign only hash of file, for example)
- MACs
- Key derivation
- Random generators

## Requirements

- Arbitary input length
- Fixed, short output length
- Efficient
- Preimage resistant = one way function (find any message that hashes to h)
- Second preimage resistance = weak collision resistance (find message m2 that hashes to hash of the given message m1)
- Collision resistance

## How to build hash functions?

- Take a block cypher and create a hash function
- Deticated hash function
  - MD4 family of hash functions
    - MD5 (broken)
    - SHA-1 (broken)
    - SHA-2 (sha256, sha512, ...)
  - SHA-3
  - others
  
## Overview of SHA-1

- Uses: Merkle-Dangard consturction
- HAs 4x20 rounds = 80
- There 4 stages
  - Stage t=1 Round j=0..19
  - Stage t=2 Round j=20..39
  - Stage t=3 Round j=40..59
  - Stage t=4 Round j=60..79
- Each round has 5x32bit input A, B, C, D, E

## Merkle damgard construction

```
X=(X1,...Xn) | PAdding | Compression function

       X
       +
+------v-------+
|Padding       |
+-------+------+
        |
        |
        |   H_i|1
     512|     +-----------+
        |     |160        |
     +--v-----v-----+     |
     |Compression   |     |
     |              |     |
     +-----+---+----+     |
           |   |          |
           |   +----------+
           |160
           v
           H(x)

      + X_1
      |
+-----v------+            +
|Message     |            | H_(x-1)
|Schedule    |            +-------------+
+-----+------+            |             |
      |       W0     +----v------+      |
      +-------------->Round 0    |      |
      | 32           +-----------+      |
      |                                 |
      |       W1     +-----------+      |
      +-------------->Round 1    |      |
      | 32           +-----------+      |
      |                                 |
      |                    X            |
      |                    X            |
      |                    X            |
      |                                 |
      |       W79    +-----------+      |
      +-------------->Round 79   |      |
        32           +-----+-----+      |
                           |            |
                         XXvXX          |
                         X X <----------+
                         XX+XX
                           |
                           |
                           v
```


<img src="https://1.bp.blogspot.com/-8JncPkmFYGk/VigEawvs2HI/AAAAAAAAAPk/wbQUGmEkoVk/s1600/sha1.gif" alt="Drawing" width=300px/>

### Round function

Similar as Fristel network:

![](https://www.cs.rit.edu/~ark/fall2013/462/module03/fig3.png)

Round function:

![](https://i.stack.imgur.com/F204w.png)

- t = 1,2,3,4
- Ft are 4 different functions
- Kt are round constants

### Message schedule

![](https://image.slidesharecdn.com/fr7vk4pvsbzh6posvax0-signature-a2aefd15529654f3e87e362a46d23579b835dc4f23157856393aba9ec132c113-poli-160425153455/95/hash-function-26-638.jpg?cb=1461598732)
