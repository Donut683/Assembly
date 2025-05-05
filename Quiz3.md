# Quiz 3

Gabriel Carino
CISC211
Danish Khan
April 23, 2025

```
section .data
    x dd 5
    fmt db "Factorial: %d", 10, 0

section .text
    global _start
    extern printf

_start:
    mov ecx, [x]
    mov eax, 1

factorial_loop:
    mul ecx
    loop factorial_loop

  push eax
    push fmt
    call printf
    add esp, 8

   mov eax, 1
    xor ebx, ebx
    int 0x80


$ nano factorial_printf.asm
$ nasm -f elf32 factorial_printf.asm -o factorial_printf.o
$ gcc -m32 factorial_printf.o -o factorial_printf
$ ./factorial_printf
Factorial: 120
```
