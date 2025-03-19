# Quiz 2

quiz2.asm
  GNU nano 6.2                                                                             
section .data
    a dd 5
    b dd 3
    c dd 2
    d dd 4
    result dd 0

section .bss
    res resb 4

section .text
    global _start

_start:
    mov eax, [a]
    imul dword [b]
    mov ebx, eax
    
    mov eax, [c]
    imul dword [d]
    add eax, ebx

    mov [result], eax

    mov eax, 1
    xor ebx, ebx
    int 0x80


jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ nano quiz2.asm
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ nasm -f elf32 quiz2.asm -o quiz2.o
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ ld -m elf_i386 quiz2.o -o quiz2
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ ./quiz2
jovyan@jupyter-gcarino-40student-2esdccd-2eedu:~$ gdb ./quiz2
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from ./quiz2...
(No debugging symbols found in ./quiz2)
(gdb) run
Starting program: /home/jovyan/quiz2 
[Inferior 1 (process 1284) exited normally]
(gdb) info variables
All defined variables:

Non-debugging symbols:
0x0804a000  a
0x0804a004  b
0x0804a008  c
0x0804a00c  d
0x0804a010  result
0x0804a014  __bss_start
0x0804a014  _edata
0x0804a014  res
0x0804a018  _end
(gdb) x /1dw 0x0804a010
0x804a010:      0
(gdb) 
