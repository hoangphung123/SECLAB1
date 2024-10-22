# Lab #1,20110370, Phung Huy Hoang, INSE331280E_02FIE
# Task 1: Buffer overflow attack
This Lab aims to exploit a buffer overflow vulnerability to attack and modify the /etc/hosts file
**Question 1**: 
- Compile asm program and C program to executable code. 
- Conduct the attack so that when C executable code runs, shellcode will be triggered and a new entry is  added to the /etc/hosts file on your linux. 
  You are free to choose Code Injection or Environment Variable approach to do. 
- Write step-by-step explanation and clearly comment on instructions and screenshots that you have made to successfully accomplished the attack.
**Answer 1**:
## 1. Create a text file named `Lab1.c` containing the vulnerable c code:

<img width="500" alt="Screenshot" src="https://github.com/hoangphung123/SECLAB1/blob/master/img/Lab1.png?raw=true"><br>