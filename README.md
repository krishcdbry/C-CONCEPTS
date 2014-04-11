C-CONCEPTS
==========

Some important concepts in C


Some important concepts in C

1. An EXE file contains two important areas or segments known as text (or code) and data. This is true with majority of executable file formats. That is, if a C file is compiled either in Windows or Linux the resultant executable file bound to contain these two segments.
2. Turbo C generates statically linked EXE files. Thus, if we copy our EXE file to another Windows machine (of course not 64 bits version windows) where Turbo C is not installed, the EXE file is going to run as it contains whatever it needs because of static linking.
3. Turbo C generated EXE file cannot directly run on other operating system like Unix/Linux
4. If OS (Windows) is not at all there in the machine, can I run this EXE file?. No. OS is needed to run an EXE file.
5. Statically linked EXE files wastes hard disk space and RAM as multiple copies of functions will be seen in HD with each EXE file and also in RAM. To correct this dynamic link libraries are used. When dynamic linking is used (programs such as Microsoft or VC++ we can use either static linking or dynamic linking) the resulting EXE file occupies less HD space and RAM when loaded. However, it needs respective DLL file to be available to run and the readymade functions code will not be seen in EXE files. While EXE files are running then only standard library functions are loaded into RAM from DLL if they are not in RAM. Main benefit of Dynamic linking is that programs gets loaded quickly as their EXE files sizes are less. 
6. In order to run a dynamically linked EXE file, we have to have all DLL’s from which it has used functions. 
7. “xxxx DLL is missing. This application will not run” error comes if DLL is missing that is used while generating our EXE file from our source( c ) programs. Of course, if DLL versions are not matching also we may get similar error
8. The following programs gives run time error. It happily compiles and runs also. 
#include<main>
int main()
{
int x;
scanf(“%d”, x);
printf(“%d\n”,x);
return 0;
} 
Here, x is declared and its value is some garbage value. In scanf, in x’s place its garbage value is taken. Thus, scanf assumes it has to read an integer and store in the memory that is pointed by that garbage value. What is the guarantee that that memory is allocated to us by OS. If not, on behalf of us, scanf is trying to store there whatever we enter from keyboard. Thus, violating OS memory system management rule. Thus, we may get error like “memory segment violation”.
9. Unix/Linux is more secure than windows. Because of this, many organizations like SBI are using Unix/Linux as backend where databases are installed while because of easiness Windows is used as frontend.
10. In India, organizations which are having more computers are: SBI, LIC. 
11. Does this program get compiled?
#include<main>
int main()
{
char x[20]=”%d%d%d’, y[20]=”%d\n%d\n%d\n”;
int p,q,r;

scanf(x, &p, &q, &r);
printf(y, p,q,r);
return 0;
} 
This program happily gets compiled and runs also. Both scanf, printf functions needs their first argument as string. Usually, we supply string constants like ”%d%d%d’. Here, we are using string variables x, y. 

Example: Similarity, here in call we are using constant and in the other variable.
X=sqrt(2); // here 2 is constant
Y=2
X=sqrt(Y); // here we are sending Y means, really 2 we are sending to sqrt. 

12. GIS: Geographic information system
13. World trade center attack taught the importance of data to the world.
14. Data is more importance than SW. SW can be re-created while data is not. Thus, data is more important. 
15. Why do need arrays? I did not ask you what is an array?. Question is why do we need arrays. The answer is: to reading data once and using the same any number of times. That is, to reduce I/O bandwidth of our programs.
16. What are the advantages of dynamic arrays? Or what are the drawbacks of language supported arrays is C?
a. Our programs lacks flexibility.
b. Our program may waste memory
c. Memory management will be in the hands of programmer when dynamic arrays.
17. Dynamic arrays can be created while program is running. We can create that much memory what we need. Neither more nor less. 
18. Functions malloc(), calloc() are used to allocate memory, while free() is to free memory. Calloc() initializes memory to 0s.
19. How to create a dynamic integer array with n elements?
int *a,n;
scanf(“%d”, &n); 
a=(int*)malloc(n*sizeof(int));
This memory can be de-allocated at any time we want.
Its life is whole life of the program or till we free it.
20. What is the use of (int *) in the above statements?
It is typecasting. Malloc allocates a chunk of memory. We can see it as an integer array or float array or character array. If you want to see it as integer array the returned generic address has to be typecasted to integer address. It is like giving a plain cloth to a tailer and asking him to stich either shirt and Fant, or lungi and kurta, or something. We give his a rectangle shaped cloth and from that he can stitches what ever we want. In the same fashion, malloc allocates a plain chunck of consecutive memory which we can see the way we like by appropriately typecasting the returned generic address from malloc. 
21. Language supported array names such as “a in int a[10];” is also a pointer. But it is appropriate to call as constant pointer. On this we cannot apply a++,--a etc,where as on dynamic pointers like in question 19, we can apply these operators. 
22. While reading data into a string variable using scanf we don’t apply & to string variable name string variable name itself pointer. It is a 1-D character array. Array name itself pointer.
23. ACM: Association of computing Machinery, a voluntary body. It organizes international level competitive test “International collegiate Programming Contest”. Prepare for it.
24. Dangling Memory: Memory that is allocated in our account but we don’t have freedom to use the same. This wastes the available memory. This situation arises when we allocate dynamic arrays in functions and we simply return from the function like the following:

void ABC(int n)
{
int *a;
a=(int *)malloc(n*sizeof(int));
…..
…..
…..
}
When we call this function ABC() with some integer as argument, it allocates dynamic integer array with that many elements. As it does not return the address of dynamic array that is created, we will not be having freedom to use the same in main or in some other functions. It is like this. Let I have asked someone to book a ticket for my travel. I gave him money. He booked and informed about the booking. But he did not hand over the ticket? What is my situation? My money is spent and yet I cannot travel as I don’t have ticket. Like the same manner, though memory is allocated in a function, unless its starting address is known, no function including main can use that memory. It becomes a waste. To get rid off this, we have return the starting address to callee function. That is, add the following line in the function probably before the closing curly brace.
return (a);

That is,
void ABC(int n)
{
int *a;
a=(int *)malloc(n*sizeof(int));
…..
…..
return (a);
}
int main()
{
int *p;
p=ABC(100);
}

Dangling error is not going to give any run time or compile time error. Rather it simply wastes the memory. It is logical error. Thus, we have to write code such that it is free from dangling memory problems.
25. Dangling Pointer: This is the one which points to memory which is not currently in our account. Consider the following code fragment.
int *a,n;
scanf(“%d”,&n);
a=(int *)malloc(n*sizeof(int));
Assume that memory starting from 22212 is allocated through malloc. Thus, a value becomes 22212. If we call free like
free(a);
All the memory that is from 22212 is de-allocated. However, a value is still 22212. That is, a is pointing to memory 22212 which is not in our account. That is, a is now called as dangling pointer. Any attempt to access that memory using a gives memory segment violation. To avoid this, soon after freeing memory that is pointer by a pointer variable say a, it has to be initialized to 0 or NULL. Also, while accessing memory via pointers we can have a check whether it is meaningful address or not with a simple if and then access memory like
if(a) {
}
By chance a is 0, we will not be executing the block. This is the recommended practice is c coding.

26. Buffer over flow problems:
Consider the following example:
char x[4]=”Raman”; 
printf(“%s\n”, x);
Is “Raman” will be printed or only “Ram” is printed? Because, we are asking 4 bytes only for x. In reality, Raman will be printed. Because, memory is allocated generally in multiples of 8 bytes or 12 bytes by the garbage collector (a memory manager). Thus, even though 4 bytes are asked it may allocates 8 or 12 bytes. C does not check whether we storing only 4 bytes or not. Thus, we may store Raman though x size is declared as 4. This is called as buffer overflow problem.

Virus developers tries to store their harmful code this type of places where checking is not done.

Java is strongly typed language where as c is not.

27. (Lary Pace) Google success is Algorithm success. Even today, the google search algorithm is superior to Micrsoft and yahoo. 
28. Bill Gates is popular for his operating system.
29. Abdul kalam advise dream big. 
30. OOPS use: code reusability, ease of coding 
In C language, we cannot have more than function with same name.
Easiness: in C language we need to remember abs(), fabs(), dabs() function names to calculate absolute value of an integer or float or double. In C++, we can have functions with same name but differing in number of arguments or argument type. Thus, we can have the following set of functions such that we can use abs() to calculate absolute of any type argument. No need of remembering many functions such as abs, fabs, dabs etc in c.

int abs(int n)
{
return ( n<0?-n:n);
}
float abs(float n)
{
return ( n<0?-n:n);
}
double abs(double n)
{
return ( n<0?-n:n);
}
This way having more than one function with same name is called as function name overloading. It is also called as compile time polymorphism or compile time binding as during the compilation time itself which version of the functions has to be really called from the argument type.

A c is weakly typed language unlike Java. C supports automatic promotion and demotion.
If integer version of abs is not there and yet we call abs with an integer argument then system invokes float version of abs in its place by promoting int argument to float. Similar line demotion takes place.

Library: contains set of functions.
In C++, we have a readymade library known as algorithm library which contains many overloaded functions. We need to include <algorithm> to use them

Code reusability: function templates. We do have class templates.
Application templates are available in Windows compilers
Standard template library is available in GNU C++ or in C++
An example function template:
Template<class A>
A abs(A n)
{
return ( n<0?-n:n);
}

Whenever we call abs with some argument, code is generated from the template function. Template means model. It is more like stencil.

Data Abstraction:
Concrete can be measured.
Abstract things cannot be possibly measured.
Gandhism is a good example for abstract things.

I can say mathematical concept of integer is abstracted in C or C++ or Java as whatever operations are meaningful in mathematics on integers the same thing are applicable on int type variables. If we ass two integers we get an integers both in mathematics and in our language also. Thus, we can say that int type abstracted integers of mathematics. If abstraction is possible, program development and understanding becomes natural.

Similarly, in mathematics if A, B are integers we can add with C=A+B, where C is again result. Is this is possible in C?. No. Of course we can represent vectors with a 1-D arrays. However, we cannot write C=A+B; assuming A,B,C are 1-D arrays in C. However, in C++ we can write a class which makes the above becomes possible.

In FORTRAN, if A,B,C are vectors, we can say C=A+B. That is, we can say FORTRAN has abstracted vectors where as C is not.

If abstraction is done programming becomes natural.

In CSE, another important area is Natural Language processing. Some features of MS Word such as word completion is the outcome of NLP research.
31. Program stack: When a program is loaded into memory an executable structure with command line arguments, text segment, data segment, stack segment, and heap segment is created in virtual memory. 
32. Virtual memory is really hard disk only. It is called as swap partition also.
33. Whenever we call a function, memory of its formal arguments and scratch variables is allocated. When we leave that memory is de-allocated. This is, taken from the stack segment of our program.
A program in swap partition:
Command line arguments, environment variables
Text
Data
Stack
Heap

34. Consider the following functions
F()
{
….
} 
Xyz()
{
..
F();
…
}
Pqr()
{
…
..
Xyz();
}
main()
{
Pqr();
}
For each function call some memory is taken from stack part. A special structure known as activation frame or stack frame is created. If stack area space gets exhausted, we get stack overflow problem. Usually recursive functions suffers from this stack overflow problem.
