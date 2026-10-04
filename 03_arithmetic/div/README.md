# Division Operation

## div1.asm
Which flags are set or cleared?

The operation is:

Dividend = 100
Divisor  = 7

100 ÷ 7 = 14 remainder 2

For an 8-bit divisor (BL), the DIV instruction divides the 16-bit value in AX by the 8-bit value in BL.

Before division:
AX = 100
BL = 7

The instruction:
div bl
produces:

AL = 14    ; quotient
AH = 2     ; remainder

CF = Undefined
ZF = Undefined 
SF = Undefined 
OF = Undefined 
PF = Undefined 
AF = Undefined
The later XOR EBX, EBX changes flags before the program exits: it clears CF and OF, clears SF, sets ZF and PF, and leaves AF undefined.

## div2.asm

Which flags are set or cleared?

The operation is:

Dividend = 50000
Divisor  = 300

50000 ÷ 300 = 166 remainder 200

Before the division:

AX = 50000
DX = 0
BX = 300

The instruction:
div bx
uses the combined DX:AX as the dividend:

DX:AX = 0000:50000

The result is:
AX = 166     ; quotient
DX = 200     ; remainder
All flags are undefined.
The program later executes-
xor ebx, ebx

## div3.asm
Which flags are set or cleared?
All flags are undefined.
The operation is:

Dividend = 300,000,000
Divisor  = 1,000

300,000,000 ÷ 1,000 = 300,000 remainder 0

The result is:
EAX = 300,000    ; quotient
EDX = 0         ; remainder