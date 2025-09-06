# Memory and Addresses (Using C)

This repository containes the learnings about memory and addresses using the C programming language. It contains topics such as pointers, memory allocation and address manipulation in a 16 bit architecture

## Index
- <a href="#hex">Hexadecimal Conversion</a>
- <a href="#mem">Memory cell</a>
- <a href="#res">Resident Memory</a>
- <a href="#seg">Segmentation of memory</a>
- <a href="">Data types in C</a>
- <a href="">Pointers</a>

## <h2 id="hex">Hexadecimal Conversion</h2>
| Hexadecimal | Decimal | Binary  |
|-------------|---------|---------|
| 0           | 0       | 0000    |
| 1           | 1       | 0001    |
| 2           | 2       | 0010    |
| 3           | 3       | 0011    |
| 4           | 4       | 0100    |
| 5           | 5       | 0101    |
| 6           | 6       | 0110    |
| 7           | 7       | 0111    |
| 8           | 8       | 1000    |
| 9           | 9       | 1001    |
| A           | 10      | 1010    |
| B           | 11      | 1011    |
| C           | 12      | 1100    |
| D           | 13      | 1101    |
| E           | 14      | 1110    |
| F           | 15      | 1111    |

<br>
<img width="665" height="582" alt="image" src="https://github.com/user-attachments/assets/caad9150-ccd7-4d5c-a4ef-608a9679f704" />


<img width="669" height="207" alt="image" src="https://github.com/user-attachments/assets/305dec0f-c93d-4037-89df-61b2e643dc13" />


## <h2 id="mem">Memory cell</h2>
Entire RAM has been divided in numbers of equal parts, which are known as memory cells. Following diagram represents the 256 MB of RAM.<br><br>
<img width="639" height="518" alt="image" src="https://github.com/user-attachments/assets/1002dda8-6d40-4eab-8663-163702b5c539" />

<br><br>
Each cell can store one-byte data. Data are stored in the binary number system. 

That is a `character` data reserves `one byte` and `integer` data reservers `two bytes` while `floating` data reserves `four bytes` memory cells. Each memory cell has unique address. 

Address is always in whole number and must be in increasing order.

For now let's assume:-
```bash
int a = 4;
```
<img width="697" height="157" alt="image" src="https://github.com/user-attachments/assets/04649d15-7a9c-4e3c-a52b-adbbf4c1fb9b" />
<br>
If 0x5000 is the address of the memory cell where value 4 is stored. Address of next memory cell will be 0x5001 and so on in increasing order. Addresses are in a continuous order
<br><br>

## <h2 id="res">Resident Memory</h2>
Ram is diivided into two parts: 
- Resident memory 
- Extended memory (useless for now)

<img width="582" height="411" alt="image" src="https://github.com/user-attachments/assets/5589d8e1-a1ed-4610-b5f0-78de24113dd6" />


Resident memory is the portion of a computer's memory that is currently being used by the operating system and active applications. It is the memory that is "resident" in the RAM (Random Access Memory) and is readily accessible for processing tasks.

When any program is executed it is stored in the residence memory. For turbo c 3.0, it has 1MB residence memory i.e. when we open turbo c 3.0 it stores 1MB in the RAM. 

## Physical address of computer  
All the c variables are stored in the residence memory. In turbo C 3.0, 20 bits address of the memory cell is known as physical address or real address. In 20 bits, we can represent address from 0x00000 to 0xFFFFF. That is all c variables must have memory address within this range.

<img width="649" height="547" alt="image" src="https://github.com/user-attachments/assets/d5f76584-9e9d-4a65-9d46-db4fc1d77264" />

<br><br>
A C programmer cannot not decides what will be the memory address of any variables he defines. It is decided by compiler. 

For Example: -

What will be output of following c code? 

```c
#include<stdio.h> 
int main(){ 
int a; 
printf("%x",&x); 
return 0; 
}

#apmersand(&) is used to get the address of variable.
``` 

<b>Output:</b> We cannot predict.

It may be 0x12345 or 0x54321 or any other address within the range of 0x00000 to 0xFFFFF. 

But we can say in 16 bits compilers address must be within 0x0000 to 0xFFFF and in 32 bits compilers memory address must be within 0x00000000 to 0xFFFFFFFF.

<b>Note:</b> <i>Suppose your c compiler is based on the microprocessor where total address buses are 32 then its total size of addressable memory will be:</i>
<div align="center">

`Addressable Memory = 2 ^ (Number of Address Bus)`
</div>

= 2^32 bytes<br>
= 4GB

## <h2 id="seg">Segmentation of memory</h2>

Residential memory of RAM of size 1MB has divided into 16 equal parts. These parts is called segment.

Each segment has size is 64 KB. 

16 * 64 KB = 1 MB <br>
(2^4 * 2^6 * 2^10) bits = 2^20 bits = 1 MB<br><br>

<img width="546" height="301" alt="image" src="https://github.com/user-attachments/assets/d7d2f850-8d8b-459e-9ced-abb2cdc3d046" />


This process of dividing memory into segments is called "segmentation of memory".

<b>NOTE:</b>Physical addresses of any variables are stored in the 20 bits. But we have not any pointers of 
size 20 bits. <br>
So pointers cannot access whole residence memory address.To solve this problem we there are three types pointers in c language. They are:-

   1. Near pointer 
   2. Far pointer 
   3. Huge pointer

## Offset address meaning 
Each segment has divided into 2 parts. They are:-
- Segment number (4 bit)
- Offset address (16 bit)
<br><br>
<img width="472" height="140" alt="image" src="https://github.com/user-attachments/assets/70eae3e8-beb0-4e6c-969e-561b24b08f6d" />


### Example
Suppose physical address of any variable is 0x500F1.<br>
Then its segment number and offset address is:-
- Segment number = 5
- Offset address = 00F1

<b>Write a program to find the offset address of any variable</b>
```c
#include<stdio.h>
int main(){
    int x;
    printf("%u ",&x);  //To print offset address 
printf("%p ",x);      //To print segment address 
printf("%p ",&x);    //To print offset address 
printf("%fp ",&x);  //To print segment address : offset address 
return 0; 
}
```

## Data segments in c language (64 KB each)
<img width="572" height="501" alt="image" src="https://github.com/user-attachments/assets/21ccd119-3c19-44ce-899b-8830cbed76cd" />


All the segments are used for specific purpose.<br>
We will discuss about how to access text video memory, graphics video memory in the pointer and union chapters of 255 bits color graphics programming.

## Data Segment (8th segment)
Segment number eight has special importance. It is called data segment. All the c variables are stored in this segment.

<b>This segment has been divided into four parts</b>.<br><br>
<img width="653" height="187" alt="image" src="https://github.com/user-attachments/assets/7583705b-b093-43a9-91bf-e81173275739" />


### 1. <u>Stack area </u>
All automatic variables and constants are stored into stack area. <br>Automatic variables and constants in c:-
1. All the local variables of default storage class. 
2. Variables of storage calls auto. 
3. Integer constants, character constants, string constants, float constants 
etc in any expression. 
4. Function parameters and function return values.

<br>
<b>NOTE:</b> Variables in the stack area are always deleted when program control reaches it out of scope. Due to this stack area is also called <i><b>temporary memory area</i></b>.

#### Example 1
What will be output of following c code? 
```c
#include<stdio.h> 
int main(){ 
int i; 
for(i=0;i<3;i++){ 
int a=5; 
printf("%d",a); 
} 
return 0; 
} 
```
<b>Output:</b>  5 5 5 

<b>Explanation:</b> Since variable `a` is automatic variable, it will store in the stack area. Scope of variable `a` is within for loop. So after each iteration variable a will be deleted from stack and in each iteration variable a will initialize. 

#### Example 2
What will be output of following c code? (Turbo C 3.0) (LIFO)
```c
#include<stdio.h> 
int main(){
    int a =5, b = 6, c = 7,d =8; 
printf("%d %d %d"); 
return 0; 
} 
```

<b>Output:</b> 8 7 6 

<b>Explanation:</b> Default storage class of variables a, b, c and d is auto .Since it automatic variable it will be sorted in the <i><b>stack</i></b> area of memory. It will store in the stack as
<div align="center">
<img width="177" height="122" alt="image" src="https://github.com/user-attachments/assets/bdbecaa8-5f14-4e08-a3ef-0bb9a9108626" />

</div> 
Stack always follows LIFO data structure. In the printf function, name of 
variables is not written explicitly. So default output will content of stack 
which will be in the LIFO order i.e. 8 7 6.
<br><br>
<b>NOTE:</b> It has two part one for initialize variable another for non-initialize variable. All initialize variables are more nearer than non-initialized variable and vice versa. For example:-

#### Example 3
What will be output of following program? (Turbo c 3.0) (LIFO) 
```c
#include<stdio.h> 
int main(){ 
int a =5, b, c =7; 
printf("%d %d %d"); 
return 0; 
} 
```
<b>Output:</b> 7 5 garbage value 

<b>Explanation: </b> Automatic variable a and c has initialized while b has not initialized. 
Initialize variables are more nearer than uninitialized variable .They will be stored in the stack. So due to LIFO first output will be 7 then 5 (since a is more nearer than b with respect to c) then any garbage value will be 
output which is present in the stack. 

<b>NOTE:</b > Default storage class of any local variable is auto

### 2. <u>Data Area</u>
All the static variables and global variables are stored in the data area. It is permanent memory space and variable will store in the memory usless and until prgogram ends.

#### Example 1
What will be output of following c code? 
```c
#include<stdio.h> 
int main(){ 
int i; 
for(i=0;i<3;i++){ 
static int a=5; 
printf("%d",a); 
} 
return 0; 
} 
```
<b>Output:</b> 5 6 7 

<b>Explanation:</b> Since variable `a` is static variable, it will store in the data area. Scope of variable `a` is within for loop. So after each iteration variable a will not be deleted from data area and in each iteration value of variable a will be incremented by 1.

### 3. <u>Heap area</u>
This memory area is used for dynamic memory allocation. All the memory allocated by malloc(), calloc(), realloc() functions are stored in the heap area. It is also permanent memory space and variable will store in the memory unless and until prgogram ends. <i>It's size is not fixed. It depends on the size of residence memory.</i>

### 4. <u>Code area</u>
This memory area is used to store the executable code of the program. It is also permanent memory space and variable will store in the memory unless and until prgogram ends. <i>It's size is fixed for the fixed size of residence memory. (1MB in this case)</i>

## <h2 id="hex">Data types in C</h2>
<img width="688" height="251" alt="image" src="https://github.com/user-attachments/assets/bb98f3af-c07e-4b2e-9d16-9309e10af1f5" />
