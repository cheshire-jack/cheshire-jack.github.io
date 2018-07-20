---
layout: post
title: "Malloc and the Heap p.1"
date: 2018-07-19
tags: linux programming C
description:  Exploring malloc, the heap, and exploitation
---
### malloc()
When programming in C we can dynamically allocate memory for objects that are created during runtime.  To do this we use a function callled _malloc()_.  This allocates memory in the heap section of program memory.  From the man page for _malloc()_ we see that it has the following attributes:

* defined in stdlib.h
* function definition: void *malloc(size_t size)
* allocates memory of size _size_
* returns a pointer to the memory if successful and a NULL pointer if not

### Using malloc()
Lets use malloc() in a program to create a linked list data structure.

```c
#include <stdio.h>
#include <stdlib.h>
(1)
struct Node {
	int data;
	struct Node *next;
};

int main(int argc, char *argv[])
{ (2)
	struct Node* head = NULL;
	struct Node* second = NULL;
	struct Node* third = NULL;
	struct Node* fourth = NULL;
	struct Node* fifth = NULL;
  (3)
	head = (struct Node*)malloc(sizeof(struct Node));
	second = (struct Node*)malloc(sizeof(struct Node));
	third = (struct Node*)malloc(sizeof(struct Node));
	fourth = (struct Node*)malloc(sizeof(struct Node));
  	fifth = (struct Node*)malloc(sizeof(struct Node));
  (4)
	head->data = 1;
	head->next = second;

	second->data = 2;
	second->next = third;

	third->data = 3;
	third->next = fourth;

	fourth->data = 4;
	fourth->next = fifth;

	fifth->data = 5;
	fifth->next = NULL;

	return 0;
}

```

This program is a simple implementation of a linked list.  We use _malloc()_ to allocate the size of each node on the heap during runtime. Lets go through the code carefully to understand what is happening.

At (1) we declare the struct for each linked list object.  Then in the _main_ function at (2) we initialize a pointer to each Node we are going to create to NULL value.  Remember here that a pointer is storing a memory address.

Next at (3) we are assigning values to each linked list node by using the fact that on success _malloc()_ returns a pointer to the allocated memory.  We take that pointer and cast it as a Node* pointer to assign it to each linked list element.  The size of the memory in this case is given by _sizeof(struct Node)_ which is the size of each Node object.  It turns out that the memory size allocated will have to be a minimum size that will contain an int value and a pointer value (typically 4 bytes and 8 bytes respectively on a 64 bit machine).

The next section of our code (4) is where we assign values to the data member of the structs and the pointer member of the strcut.

### Looking at a lower level
In this section we are going to look at what happens at the assembly level of our previous program.  I compiled the program using gcc 8.1.1 and then used Binary Ninja to look at the disassembled binary.

![malloc disassembly](/images/malloc1-0.jpg)

Starting at the address 0x624 we can see the initialization code setting the value of each node to NULL.  Then we see starting at address 0x64c moving the _size_ argument for _malloc()_ into the edi register to pass to _malloc()_ when we call the function at 0x651.  As we can see each call to _malloc()_ is allocating 16 bytes on the heap.  Then we are setting the value in rax (the return value of _malloc()_) to the allocated pointer from our previous section.

The next section starting at address 0x692 is where we start assigning values to our struct members in the linked list.  First we move the address of our node into register rax.  Then we move the value of the data member to that address.  After that we need to populate the next pointer in the struct.  To do that we store the addresses of the node we are at and the next node into rax and rdx respectively.  Then we store the next node address in rdx to rax+0x8 which is the location of the pointer storage.

### Issues using malloc()
Now that we have an idea of what _malloc()_ does and what it looks like at a lower level we can look at some mistakes that programmers can make with _malloc()_.

One mistake that can be made when using _malloc()_ is to assume that the memory is initialized when it is not.  If the memory is then used without intializing it a disclosure of data could occur.

Failing to check the return value of _malloc()_ is another mistake.  This can cause a NULL pointer dereference which can lead to an exploit.

Using memory after _free()_ is another issue which may lead to an exploitable vulnerability.  Along with using _free()_ on the same memory multiple times.

### Conclusion
Hopefully you found something useful in this post.  In part 2 I am going to go over some vulnerable code using _malloc()_ and look at how the vulnerabilities can be exploited.

### References
* [GeeksforGeeks](https://www.geeksforgeeks.org){:target="_blank"}
* [Secure Coding in C and C++](https://www.amazon.com/Secure-Coding-SEI-Software-Engineering-ebook/dp/B00C0OBZI0/ref=sr_1_1?ie=UTF8&qid=1532068474&sr=8-1&keywords=secure+coding+in+c+and+c%2B%2B%2C+2nd+edition){:target="_blank"}
* [The Linux Programming Interface](https://nostarch.com/tlpi){:target="_blank"}
