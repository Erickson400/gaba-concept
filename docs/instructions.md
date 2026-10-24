# Instructions

- All registers and keywords must be lower-case.
- Other than decimal, numbers can be binary or hex. With prefixes 0b, 0x respectively.
- Comments are //, not ;.

cc can be
    - zero
    - not zero
    - carry
    - not carry

---Opcode instructions mapped to RGBDS---
Load instructions
LD r8,r8                --- r8 = r8
LD r8,n8                --- r8 = n8
LD r16,n16              --- r16 = n16
LD [HL],r8              --- *hl = r8
LD [HL],n8              --- *hl = n8
LD r8,[HL]              --- r8 = *hl
LD [r16],A              --- *r16 = a
LD [n16],A              --- *n16 = a
LDH [n16],A             --- *hram(n16) = a
LDH [C],A               --- *hram(c) = a
LD A,[r16]              --- a = *r16
LD A,[n16]              --- a = *n16
LDH A,[n16]             --- a = *hram(n16)
LDH A,[C]               --- a = *hram(c)
LD [HLI],A              --- *hl++ = a
LD [HLD],A              --- *hl-- = a
LD A,[HLI]              --- a = *hl++
LD A,[HLD]              --- a = *hl--

8-bit arithmetic instructions
ADD A, r8.              --- a += r8
ADD A, n8               --- a += n8
ADD A, [HL]             --- a += *hl
ADC A, r8               --- a += r8 + carry
ADC A, n8               --- a += n8 + carry
ADC A, [HL]             --- a += *hl + carry
CP r8                   --- compare r8
CP n8                   --- compare n8
CP [HL]                 --- compare *hl
DEC r8                  --- r8--
DEC [HL]                --- (*hl)--
INC r8                  --- r8++
INC [HL]                --- (*hl)++
SBC A, r8               --- a -= r8 - carry
SBC A, [HL]             --- a -= *hl - carry
SBC A, n8               --- a -= n8 - carry
SUB A, r8.              --- a -= r8
SUB A, [HL]             --- a -= *hl
SUB A, n8               --- a -= n8

16-bit arithmetic instructions
ADD HL, r16             --- hl += r16
DEC r16                 --- r16--
INC r16                 --- r16++

Bitwise logic instructions
AND r8                  --- a &= r8
AND [HL]                --- a &= *hl
AND n8                  --- a &= n8
CPL                     --- a = ~a
OR r8                   --- a |= r8
OR [HL]                 --- a |= *hl
OR n8                   --- a |= n8
XOR r8                  --- a ^= r8
XOR [HL]                --- a ^= *hl
XOR n8                  --- a ^= n8

Bit flag instructions
BIT u3,r8               --- test bit u3 in r8
BIT u3,[HL]             --- test bit u3 in *hl
RES u3,r8               --- reset bit u3 in r8
RES u3,[HL]             --- reset bit u3 in *hl
SET u3,r8               --- set bit u3 in r8
SET u3,[HL]             --- set bit u3 in *hl

Bit shift instructions
RL r8                   --- rotate r8 left
RL [HL]                 --- rotate *hl left
RL A                    --- rotate a left
RLC r8                  --- rotate r8 left circular
RLC [HL]                --- rotate *hl left circular
RLC A                   --- rotate a left circular
RR r8                   --- rotate r8 right
RR [HL]                 --- rotate *hl right
RR A                    --- rotate a right
RRC r8                  --- rotate r8 right circular
RRC [HL]                --- rotate *hl right circular
RRC A                   --- rotate a right circular
SLA r8                  --- r8 <<= 1
SLA [HL]                --- *hl <<= 1
SRA r8                  --- r8 >>= 1
SRA [HL]                --- *hl >>= 1
SRL r8                  --- r8 >>>= 1
SRL [HL]                --- *hl >>>= 1
SWAP r8                 --- swap r8
SWAP [HL]               --- swap *hl

CALL n16                --- call n16
CALL cc, n16            --- call n16 if cc
JP HL                   --- goto hl
JP n16                  --- goto n16
JP cc,n16               --- goto n16 if cc
JR n16                  --- gotor n16
JR cc,n16               --- gotor n16 if cc
RET CC                  --- return if cc
RET                     --- return
RETI                    --- ireturn
RST vec                 --- goto vec

CCF                     --- invert carry
SCF                     --- set carry

ADD HL, SP              --- hl += sp
ADD SP, e8              --- sp += e8
DEC SP                  --- sp--
INC SP                  --- sp++
LD SP, n16              --- sp = n16
LD [n16], SP            --- *n16 = sp     dont like
LD HL,SP+e8             --- hl = sp + e8
LD SP,HL                --- sp = hl
POP AF                  --- pop af
POP r16                 --- pop r16
PUSH AF                 --- push af
PUSH r16                --- push r16

DI                      --- di
EI                      --- ei
HALT                    --- halt

DAA                     --- daa
NOP                     --- nop
STOP                    --- stop

All possible loads/stores:
r8 = r8
r8 = n8
r8 = *r16
r8 = *n16
r16 = r8            // Sets the high byte to 0, and lower byte to the register.
r16 = n8            // Sets the high byte to 0, and lower byte to the constant.
r16 = r16
r16 = n16
r16 = *r16          // Load two bytes in little-endian order.
r16 = *n16          // Load two bytes in little-endian order.
*hl++ = r8
*hl++ = r16
*hl++ = n16
r8 = *hl++
r16 = *hl++
*r16 = r8
*r16 = n8
*r16 = r16          / Store two bytes in little-endian order.
*r16 = n16          / Store two bytes in little-endian order.
*n16 = r8
*n16 = n8
*n16 = r16          // Store two bytes in little-endian order.
*n16 = n16          // Store two bytes in little-endian order.
*hram(c) = r8
*hram(c) = n8
*hram(c) = r16
*hram(c) = n16
*hram(c) = *r16
*hram(c) = *n16
r8 = *hram(c)
n8 = *hram(c)
r16 = *hram(c)
n16 = *hram(c)
*r16 = *hram(c)
*n16 = *hram(c)
sp = n16
sp = hl
*n16 = sp
hl = sp + e8
// *hram(n16) loads/stores can be automatically placed if the n16 is in high ram.
// If the user desires the extra space and cycles, then they should add a nop right after.
//
// Using the C or BC register with *hram(c) is invalid.
//
// Disallow using the same register for destination and source, dereferenced or not.
// Use breakpoint and debug keywords for ld b, b and ld d, d instead.

*r16 = *r16 
is ambiguis because its not known if its setting 1 byte or 2.
*bc: u16 = *de 

All possible load destinations:
n8
r8
r8++/--
n16
r16
r16++/--

All possible load sources:
*n16
*n16++/--
*r16
*r16++/--
*hram(c)
sp

All possible store destinations:
*n16
*n16: u16
*n16++/--
*n16++/--: u16
*r16
*r16: u16
*r16++/--
*r16++/--: u16
*hram(c)

All possible store sources:
n8
r8
r8++/--
n16
r16
r16++/--

I cant differentiate *n16 = n8 from *n16 = n16 because literals are untyped.
*n16 = n8 is useless since *n16 = n16 already exists
