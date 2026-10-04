# subtraction operation

## sub1.asm
Which flags are set or cleared?

The operation is:
50 - 80 = -30
In 8-bit binary:
  00110010   (50)
- 01010000   (80)
-----------
  11100010   (-30)

AL = 11100010b = E2h

| Flag | Status | Reason |
|---|---|---|
| CF (Carry Flag) | Set (1) | A borrow is required because 50 < 80. |
| ZF (Zero Flag) | Cleared (0) | The result is not zero. |
| SF (Sign Flag) | Set (1) | The most significant bit is 1. |
| OF (Overflow Flag) | Cleared (0) | -30 is within the signed 8-bit range (-128 to 127). |
| PF (Parity Flag) | Set (1) | `E2h` (`11100010b`) has four 1-bits in the low byte, so parity is even. |
| AF (Auxiliary Carry Flag) | Cleared (0) | The low nibbles `2 - 0` require no borrow from bit 4 to bit 3. |

## sub2.asm
Which flags are set or cleared?

The operation is:

1000 - 2000 = -1000

In hexadecimal:

03E8h - 07D0h = FC18h

So:

AX = FC18h

As a signed 16-bit value, FC18h represents -1000.

| Flag | Status | Reason |
|---|---|---|
| CF (Carry Flag) | Set (1) | A borrow is required because 1000 < 2000. |
| ZF (Zero Flag) | Cleared (0) | The result `FC18h` is not zero. |
| SF (Sign Flag) | Set (1) | The most significant bit of `FC18h` is 1. |
| OF (Overflow Flag) | Cleared (0) | -1000 is within the signed 16-bit range (-32768 to 32767). |
| PF (Parity Flag) | Set (1) | The low byte `18h` (`00011000b`) has two 1-bits, so parity is even. |
| AF (Auxiliary Carry Flag) | Cleared (0) | The low nibbles are `8 - 0`, so no borrow occurs from bit 4 to bit 3. |

## sub3.asm
Which flags are set or cleared?

First:
0 - 1 = FFFFh
So after SUB:

AX = FFFFh
CF = 1

Then, `SBB AX, 0`:
means:
AX = AX - 0 - CF
   = FFFFh - 0 - 1
   = FFFEh
AX = FFFEh

Flags immediately after `SBB AX, 0`:

| Flag | Status | Reason |
|---|---|---|
| CF (Carry Flag) | Cleared (0) | `FFFFh - 0 - 1 = FFFEh` requires no unsigned borrow; the minuend is greater than the effective subtrahend. |
| ZF (Zero Flag) | Cleared (0) | The result `FFFEh` is not zero. |
| SF (Sign Flag) | Set (1) | The most significant bit of `FFFEh` is 1. |
| OF (Overflow Flag) | Cleared (0) | The signed result, -2, is within the 16-bit range. |
| PF (Parity Flag) | Cleared (0) | The low byte `FEh` (`11111110b`) has seven 1-bits, so parity is odd. |
| AF (Auxiliary Carry Flag) | Cleared (0) | The low nibble calculation is `Fh - 0 - 1 = Eh`, with no borrow from bit 4 to bit 3. |