# Lab #1,20110370, Phung Huy Hoang, INSE331280E_02FIE
# Task 1: Buffer overflow attack
This Lab aims to exploit a buffer overflow vulnerability to attack and modify the /etc/hosts file
**Question 1**: 
- Compile asm program and C program to executable code. 
- Conduct the attack so that when C executable code runs, shellcode will be triggered and a new entry is  added to the /etc/hosts file on your linux. 
  You are free to choose Code Injection or Environment Variable approach to do. 
- Write step-by-step explanation and clearly comment on instructions and screenshots that you have made to successfully accomplished the attack.
**Answer 1**:
## 1. Compile asm program and C program to executable code.:
*First, Create a text file named `Lab1.c` containing the vulnerable c code:*<br>

<img width="500" alt="Screenshot" src="https://github.com/hoangphung123/SECLAB1/blob/master/img/Lab1.png?raw=true"><br>
*Then: Compile the vulnerable C program using the following command "gcc -g Lab1.c -o Lab1.out -fno-stack-protector -z execstack -mpreferred-stack-boundary=2"*<br>

```sh
gcc -g Lab1.c -o Lab1.out -fno-stack-protector -z execstack -mpreferred-stack-boundary=2
``` 
- fno-stack-protector: Disables stack protection mechanisms (canary)
- z execstack: Makes the stack executable, allowing the shellcode to run
- mpreferred-stack-boundary=2: Stack will be aligned with 2^2 = 4 bytes

*Next, Write and compile shellcode using assembly*<br>
- Create a file named `shellcode.asm`
- Compile shellcode.asm
```sh
nasm -f elf32 -o shellcode.o shellcode.asm
``` 
```sh
ld -o shellcode shellcode.o
``` 
- The command ld -o shellcode shellcode.o is used to link (link) the object file (object file) shellcode.o into an executable file named shellcode.

*Next, Extract shellcode in hex format*<br>

```sh
for i in $(objdump -d shellcode |grep "^ " |cut -f2); do echo -n '\x'$i; done;echo
``` 
- We will get the hex code as shown
