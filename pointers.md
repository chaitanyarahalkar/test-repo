## In Depth Concept: Pointers In C Programming 


Pointers are data types that point to a certain memory location storing some data. Pointers are extremely important as they give direct access to manipulate data at a given memory location.

``` int *ptr; ``` creates a pointer that is able to point to an address of a variable storing integer data.

```
int x = 10;
int *ptr = &x;
printf("Address of x=%d is %p",*ptr,&x);

```

The & operator is called as the referencing operator while * is called dereferencing operator. & returns the address of the variable containing the given data.

A pointer variable can point to integer,float,double,long & character.


Pointers can be usually of four kinds:

1.Assigned Pointers
2.Null Pointers
3.Dangling Pointers
4.Wild Pointers

1. Assigned pointers are the pointers which are pointing to a certain distinct memory location. 

2. A NULL pointer points to nothing. A pointer may be assigned NULL if an address is not yet assigned to it. It may temporarily point to NULL.

```
typedef struct node
{
	int data;
	struct node *next;
}node;
int main(void)
{

  node *head = (node*)malloc(sizeof(node));
  node *tail;
  return 0;
}

```

Here a new linked-list node is created and the pointer in the node is pointing to NULL until a new node is created. (*tail is called as an opaque pointer since nothing can be said about what data is the pointer pointing to. Opaque pointers can be assigned to NULL).

3. If a pointer is pointing to a memory location that has been deleted/freed, it is called a dangling pointer.

``` 

int *p = (int*)malloc(5*sizeof(int));
free(p);

```

In the above code snippet, p is pointing to the first block of the 5 blocks of consecutive memory locations of the size of an integer. (Malloc allows for creation of consecutive memory locations dynamically.). After using the allocated space, it is a good convention to free up the used space. After freeing up, p is a dangling pointer. 

4. A pointer which is not initialised to anything(Not even NULL) is a wild pointer.

```
int *p;

```

Here p is a wild pointer. It is not pointing to anything.(Not even NULL)


A special type of pointer exists called as the void pointer. The void pointer points to a block of memory location but the data type is not specified. A void pointer can be type-casted into any other data type.
Void pointers cannot be dereferenced. Pointer arithmetic is not possible on void pointers since the data that they are pointing to is unknown.


```
int a = 10;
char b = 'a';

void *p;
p = &a;

printf("%d",*((int*)p));
p = &b;

printf("%c",*((char*)p));


```

In the code snippet given above, a void pointer p is created. It was first made to point to a memory location storing an integer. Then the void pointer was type-casted to int*,in order to print the data in integer type format. The void pointer was then pointing to a character storing memory location. It was then type-casted to char*,to print the data in character type format.

Let us look at the commonly used swap elements example.

```
#include<stdio.h>
void swap(int a,int b)
{
	int temp = a;
	a = b;
	b = temp;
}
int main(void)
{

int x = 10;
int y = 20;
printf("Values before swap: x=%d,y=%d",x,y);
swap(x,y);
printf("Values after swap: x=%d,y=%d",x,y);
return 0;
}

```

This program won't give the desired output. This happens because when x and y are passed to the swap function, a local copy of the variables is created in a & b. The swap function then swaps the values of a and b keeping the original copies intact. Hence the correct way of doing this would be to swap the data at the actual memory locations. Here is where pointers are useful. The same program can be written correctly as: 


```
#include<stdio.h>
void swap(int *a,int *b)
{
	int temp = *a;
	*a = *b;
	*b = temp;
}

int main(void)
{
	int x = 10;
	int y = 20;
	printf("Values before swap: x=%d,y=%d",x,y);
	swap(&x,&y);
	printf("Values after swap: x=%d,y=%d",x,y);
	return 0;
}

```

In the above program, &x and &y are passed to the swap function. Thus we are passing the addresses of x and y to swap. These addresses are then pointed by the two pointers *a & *b. Now since we have direct access to the memory locations of x & y we can swap the values of the original variables. 


#### Array Pointers


Array pointers are pointers to arrays i.e consecutive blocks of memory.

```
int a[] = {1,2,3,4};
int (*p)[4];
p = &a;

printf("Element at position 2 is:%d",(*p)[1]);

```

Array pointers point to the entire array and not to the first element of the array. Note the difference between the above snippet and the code shown below

```
int a[] = {1,2,3,4};
int *p;
p = a;

printf("Element at position 2 is:%d"*(p+1));

```

Here the pointer p is pointing to the first element of the array. Random element access can be done as shown.

2 Dimensional arrays with pointers:

```
int a[2][2] = {{1,2},{3,4}};

printf("Element at 1,0:%d",*(*(a)+1));
printf("Element at 1,1:%d",*(*(a+1)+1));

```
#### Function Pointers

Just as we have pointers that point to certain data, function pointers point to a block of instructions of the function. As soon as a function pointer is assigned to a function, it points to the first instruction of the function.
The syntax of creating a function pointer is 

``` int (*fp)(); ``` 

This will create a function pointer that will point to a function that has int as its return type accepting no arguments. Removing the parenthesis around *fp ( ``` int *fp(); ``` )totally changes the meaning of the declaration. It suggests that fp is a function declaration having no arguments and returning an integer pointer.

Function pointers cannot be used to deallocate memory just as we free memory for data with free().

```
#include<stdio.h>
void foo(int x)
{
	printf("%d",x);
}
int main(void)
{
	void (*bar)(int) = &foo;

	*bar(5);
	return 0;
}

```

In the above program,bar is a function pointer pointing to the function foo. Instead of &foo,foo is also acceptable.  

#### Why are function pointers useful?

Function pointers are used for callback functioning. They are also useful to simplify code.

```

switch(foo)
{
	case 1:bar1();break;
	case 2:bar2();break;
	case 3:bar3();break;
	default:bar();
}

```
Instead of the above code snippet we may write 

```
#include<stdio.h>

void bar1()
{
	printf("bar1");
}
void bar2()
{
	printf("bar2");
}
void bar3()
{
	printf("bar3");
}
void bar()
{
	printf("bar");
}
int main(void)
{
	void (*p[])() = {bar1,bar2,bar3,bar};

	(*p[foo])();
	return 0;
}

```

Callback mechanisms are highly useful. An implementation can be found in the qsort function in C.

```
#include<stdio.h>
#include<stdlib.h>
int compare(const void *a,const void *b)
{
	return (*(int*)a-*(int*)b);
}
int main(void)
{

	int arr[] = {4,3,2,1};
	int n = 4;
	int i;
	qsort(arr,n,sizeof(int),compare);

	for(i=0;i<n;i++)
		printf("%d",arr[i]);

	return 0;
}

```
The compare function is passed as an argument to the sort function. This mechanism allows the sort function to sort any kind of data. This is the backbone of templates in C++.

