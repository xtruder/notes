# Hash functions

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

### Merkle dangard construction

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


