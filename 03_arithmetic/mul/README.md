# Multiplication

## mul1.asm
What flags are set?

The operation is:
25 × 10 = 250
In hexadecimal:
19h × 0Ah = FAh
Since this is an 8-bit multiplication:
mul byte [num2]

the processor performs:
AL × num2 → AX

AX = 00FAh
AL = FAh
AH = 00h
Flags after MUL:

| Flag | Status | reason |
|---|---|---|
| CF | Cleared (0) | The upper half of the result (`AH`) is `00h`. |
| OF | Cleared (0) | The result fits entirely in the lower 8 bits (`AL`). |
| ZF | Undefined | `MUL` does not define the Zero Flag. |
| SF | Undefined | `MUL` does not define the Sign Flag. |
| PF | Undefined | `MUL` does not define the Parity Flag. |
| AF | Undefined | `MUL` does not define the Auxiliary Carry Flag. |

Registers after MUL:

| Register | Value | reason |
|---|---|---|
| AL | `FAh` | Lower 8 bits of the product (250). |
| AH | `00h` | Upper 8 bits of the product. |
| AX | `00FAh` | Complete 16-bit product. |

## mul2.asm

What flags are set?
The operation is:

3000 × 200 = 600000

In hexadecimal:

0BB8h × 00C8h = 927C0h

Because this is a 16-bit multiplication:

mul word [num2]

the processor performs:

AX × num2 → DX:AX

Therefore:

DX:AX = 0009:27C0h

Registers after MUL:

| Register | Value | Meaning |
|---|---|---|
| AX | `27C0h` | Lower 16 bits of the product. |
| DX | `0009h` | Upper 16 bits of the product. |
| DX:AX | `0009:27C0h` | Complete 32-bit product. |

Flags after MUL:

| Flag | Status | Why |
|---|---|---|
| CF | Set (1) | The upper half of the result, `DX = 0009h`, is non-zero. |
| OF | Set (1) | The result does not fit in 16 bits, so the upper half is non-zero. |
| ZF | Undefined | `MUL` does not define the Zero Flag. |
| SF | Undefined | `MUL` does not define the Sign Flag. |
| PF | Undefined | `MUL` does not define the Parity Flag. |
| AF | Undefined | `MUL` does not define the Auxiliary Carry Flag. |

Final result:
AX = 27C0h
DX = 0009h

## mul3.asm

Operation:
100,000 × 300,000 = 30,000,000,000

Since this is a 32-bit MUL, the 64-bit result is stored across `EDX:EAX`.

EAX (lower 32 bits) = 0xFC23AC00
EDX (upper 32 bits) = 0x00000006
EDX:EAX = 0x00000006FC23AC00

| Flag | Status | Why |
|---|---|---|
| CF | Set (1) | `EDX` is non-zero, meaning the result does not fit in 32 bits. |
| OF | Set (1) | `EDX` is non-zero, so the upper half of the product is not zero. |
| ZF | Undefined | `MUL` does not define ZF. |
| SF | Undefined | `MUL` does not define SF. |
| PF | Undefined | `MUL` does not define PF. |
| AF | Undefined | `MUL` does not define AF.