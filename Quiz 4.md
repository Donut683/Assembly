# Quiz 4

Gabriel Carino
Professor Khan 
CiSC211

```
section .data
    x dd 10
    y dd 20
    z dd 30
    result dd 0

section .text
    global _start

_start:
    push dword [z]
    push dword [y]
    push dword [x]
    call add_three
    add esp, 12
    mov [result], eax
    mov eax, 1
    mov ebx, 0
    int 0x80

add_three:
    push ebp
    mov ebp, esp
    mov eax, [ebp + 8]
    add eax, [ebp + 12]
    add eax, [ebp + 16]
    pop ebp
    ret

```
