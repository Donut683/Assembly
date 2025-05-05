# Midterm
Gabriel C
3/26/2025
CISC211
Professor Danish Khan

```
1.  Write an x86-compatible assembly code that calculates the
following equation.

arith.asm
section .data
var1 dd 10
var2 dd 30
var3 dd 8
result dd 0
msg db  "Result: ", 0
newline db 10

section .bss
buffer resb 4

section .text
global _start

_start:
mov eax, [var1]
add eax, [var2]
xor edx, edx
div dword [var3]
mov [result], eax
add eax, '0'
mov [buffer], al
mov eax, 4
mov ebx, 1
mov ecx, msg
mov edx, 8
int 0x80
mov eax, 4
mov ebx, 1
mov ecx, buffer
mov edx, 1
int 0x80
mov eax, 4
mov ebx, 1
mov ecx, newline
mov edx, 1
int 0x80
mov eax, 1
xor ebx, ebx
int 0x80


jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ nano arith.asm
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ nasm -f elf32 arith.asm -o arith.o
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ ld -m elf_i386 arith.o -o arith
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ ./arith
Result: 5

1c — Register Table

| Register |  Value |
|----------|--------|
| `EAX`    |  `5`   |
| `EDX`    |  `0`   |

Verified using `gdb`:
bash
gdb ./arith
run
info registers

EAX = 5
EDX = 0


2. K-Map simplification
Y = a·b + a'·b + a·b'

1.a*b + a'*b = b(a + a') = b (group terms)
2.Y=b + a*b' (combine remaining terms)
3.Y=b + a*b' (final expression)

3.Write a code that identifies an odd or an even number

oddnumber.asm
section .data
    num dd 7
    msg_even db "even number", 10
    len_even equ $ - msg_even
    msg_odd db "odd number", 10
    len_odd equ $ - msg_odd

section .text
    global _start

_start:
    mov eax, [num]
    xor edx, edx
    mov ecx, 2
    div ecx
    cmp edx, 0
    je even_number

odd_number:
    mov eax, 4
    mov ebx, 1
    mov ecx, msg_odd
    mov edx, len_odd
    int 0x80
    jmp exit

even_number:
    mov eax, 4
    mov ebx, 1
    mov ecx, msg_even
    mov edx, len_even
    int 0x80

exit:
    mov eax, 1
    xor ebx, ebx
    int 0x80


jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ nasm -f elf32 oddnumber.asm -o oddnumber.o
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ ld -m elf_i386 oddnumber.o -o oddnumber
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ ./oddnumber
odd number
```
