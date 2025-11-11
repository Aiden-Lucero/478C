# 478 Lab 06 Shellcode Demonstration Lab
1. Aiden Lucero
2. ID: 028596904

Platform: Ubuntu 24.04 in Docker

Commands Used to Compile: 
1. nano server.c -> gcc -o echo_server server.c
2. nano client.c -> gcc -o echo_client client.c
3. nano hello64.s -> gcc -no-pie -o hello64 hello64.s

Commands to run:
1. Terminal A: ./echo_server
2. Terminal B: ./hello64
3. Terminal C: ./echo_client

<img width="3839" height="2018" alt="image" src="https://github.com/user-attachments/assets/af249f05-8e42-4edb-b6b4-7145e4ef38ae" />


Explanation: 
All the files were created inside Docker and perfectly compile and run. Using the skeleton code helped me build the server and implement a safe echo server that listens for any client connection and echoes a message that is sent. The client code is meant to connect to the server, send the user's input, and display the server's response. This design is safe because it uses system calls, which avoid random input, and only echoes text that is received by the user instead of executing unnecessary operations. The assembly code uses a call-pop technique, that prints a message without relying on the C runtime. 

Assembly demo: 

   .section .text
   .global _start

_start:
    jmp message

code:
    pop    %rsi
    mov    $1, %rax
    mov    $1, %rdi
    mov    $msg_len, %rdx
    syscall

    mov    $60, %rax
    xor    %rdi, %rdi
    syscall

message:
    call code
    .ascii "Hello from CECS478 Lab06 Aiden Lucero 028596904\n"
msg_len = . - message - 5
