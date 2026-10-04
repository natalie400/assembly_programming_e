# Addition Operations

## for add1.asm

Which flags are set or cleared?

The operation is:

num1 = 120 = 01111000b
num2 = 10  = 00001010b

  01111000
+ 00001010

-----------
  10000010

Therefore:

AL = 10000010b = 130
Flags after `ADD AL, [num2]`:

| Flag | Status | Reason |
|---|---|---|
| CF (Carry Flag) | Cleared (0) | There is no carry out of the 8-bit range. 120 + 10 = 130, which is less than 256. |
| ZF (Zero Flag) | Cleared (0) | The result, `10000010b`, is not zero. |
| SF (Sign Flag) | Set (1) | The most significant bit of the result is 1. |
| OF (Overflow Flag) | Set (1) | Both operands are positive, but 130 is outside the signed 8-bit range of -128 to 127. |
| PF (Parity Flag) | Set (1) | The result `10000010b` contains two 1-bits, an even number. |
| AF (Auxiliary Carry Flag) | Set (1) | The low nibbles add to `8h + Ah = 12h`, producing a carry from bit 3 to bit 4. |



## for add3.asm
Which flags are set or cleared?

After ADD AX, [num2]

The operation is:

AX = FFFFh
num2 = 0001h

FFFFh + 0001h = 1 0000h

| Flag | Status | Reason |
|---|---|---|
| CF (Carry Flag) | Set (1) | A carry was produced because `FFFFh + 1` exceeds the 16-bit range. |
| ZF (Zero Flag) | Set (1) | The 16-bit result is `0000h`. |
| SF (Sign Flag) | Cleared (0) | The most significant bit of `0000h` is 0. |
| OF (Overflow Flag) | Cleared (0) | There is no signed overflow because `FFFFh` represents -1 and adding 1 gives 0. |
| PF (Parity Flag) | Set (1) | `0000h` has zero 1-bits in its low byte, which is even parity. |
| AF (Auxiliary Carry Flag) | Set (1) | A carry occurs from bit 3 to bit 4 when adding `Fh + 1`. |

After ADC AX, 0

ADC adds the carry flag from the previous operation:

AX = 0000h
CF = 1

The final result is 0001h.

| Flag | Status | Reason |
|---|---|---|
| CF (Carry Flag) | Cleared (0) | `0000h + 1` does not produce a carry out of the 16-bit range. |
| ZF (Zero Flag) | Cleared (0) | The result is `0001h`, not zero. |
| SF (Sign Flag) | Cleared (0) | The most significant bit of `0001h` is 0. |
| OF (Overflow Flag) | Cleared (0) | There is no signed overflow; the result `0001h` is within the signed range. |
| PF (Parity Flag) | Cleared (0) | `0001h` has one 1-bit in its low byte, which is odd parity. |
| AF (Auxiliary Carry Flag) | Cleared (0) | There is no carry from bit 3 to bit 4. |


## for add2.asm

Which flags are set or cleared?

After `ADD AX, [num2]`:

num1 = 32000 = 7D00h
num2 =   500 = 01F4h

  7D00h
+ 01F4h
-------
  7EF4h = 32500


| Flag | Status | Reason |
|---|---|---|
| CF (Carry Flag) | Cleared (0) | There is no carry out of bit 15; the result fits in 16 bits. |
| ZF (Zero Flag) | Cleared (0) | The result, `7EF4h`, is not zero. |
| SF (Sign Flag) | Cleared (0) | The most significant bit of the 16-bit result is 0. |
| OF (Overflow Flag) | Cleared (0) | The positive signed sum, 32500, is within the 16-bit signed range of -32768 to 32767. |
| PF (Parity Flag) | Cleared (0) | The low byte is `F4h` (`11110100b`), which has five 1-bits (odd parity). |
| AF (Auxiliary Carry Flag) | Cleared (0) | The low nibbles add to `0 + 4`, with no carry from bit 3 to bit 4. |

These are the flags immediately after `ADD`. The following `XOR EBX, EBX` changes some flags before the program exits.