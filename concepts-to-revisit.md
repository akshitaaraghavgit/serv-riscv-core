# How the 1 bit ALU of SERV works?
Example:
```
li x1, 5
li x2, 8
add x3, x1, x2
```
```
5  = 0101
8  = 1000
------------
13 = 1101
```
SERV's 1-bit ALU processes:
```
bit 0 → bit 1 → bit 2 → ... → bit 31
```
- It has a full adder
- SERV takes the bits from right to left.
  ```
  1 (from 5) + 0 (from 8) = 1
  1 + 0 + carry 0 = 1
  0 + 1 + carry 0 = 1
  ```
- RESULT
  ```
  1101 = 13
  ```
  ## Where does the flip-flop come in?
  ```
  1 + 1 = 10
  ```
  - the adder would produce carry = 1, and the flip-flop would store that 1 so that the next bit can use it.
  ```
          5       8
        ↓       ↓
       0101    1000
        ↓       ↓
        └──→ ADDER
              ↓
           result bit
              ↓
           1101 (13)

      carry = 0
         ↓
    FLIP-FLOP
         ↓
   stores 0 for next bit
  ```
