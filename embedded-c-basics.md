# Embedded C Notes

## printf()

### Understanding Right to Left Evaluation of printf()
In printf(), the order in which events happen is as follows:
1. **Evaluation** happens first AND from **right to left**
2. Fitting in evaluated values into the placeholder, basically th e **actual printing** happens second AND printing order remains **left to right** (as specified)

#### Example 0: Understanding Example
```c
#include <stdio.h>

int a() {
    printf("a has run!\n");
    return 7;
}

int b() {
    printf("b has run!\n");
    return 13;
}

int main()
{
    printf("%d, %d\n", a(), b());
}
```
```
Output:
b has run!
a has run!
7, 13
```
**Comment:** the lines `b has run!` and `a has run!` indicate the order of evaluation is from right to left, while the printed order of `7,13` is as we specified from left to right


#### Example 1: Post and Pre Increment/Decrement
```c
int x;
    
    x = 20;
    printf("%d, %d\n", x++, x);

    x = 20;
    printf("%d, %d\n", x, x++);
```
```c
Output:
20, 21
21, 20
```

#### Example 2
```c
    int a = 15;
    int b = 17;
    printf("a is %d, b is %d",a,b);
```
```
Output:
a is 15, b is 17
```

#### Example 3 (Conversion: Number System)
```c
int base16 = 15;
 printf("Hexadecimal value:\t %x \n", base16);
 printf("Octal Value:\t %o \n", base16);
 printf("Decimal Value:\t %d \n", base16);
 ```
```
Output:
Hexadecimal value:       f 
Octal Value:     17 
Decimal Value:   15
```
## scanf()
```c
#include <stdio.h>

int main()
{
   int a;
   scanf("%d", &a);
   printf("a = %d",a);
}
```
```
Output:
3
a = 3
```
* `&variable_name` is compulsory
* Based on type of data input, change the placeholder (%d, %f, %c, %s)

## Conditional Operator 
Conditional operator `exp1 ? exp2 : exp3` prints exp2 if exp1 is true and prints exp3 if exp1 is false
```c
    int a=3, b=2;
    int out = (a<b)?(a*a):(b-b); 
    printf("%d", out);
```
```
Output:
0
```

## Shift Operators
`x >> n` : **Right shift x by n bits** 
* Every time x is shifted right by 1 bit it is **divided by 2**
* To divide by 8, `x>>3`

`x << n` : **Left shift x by n bits**
* Every time x is shifted left by 1 bit it is **multiplied by 2**
* To mulitply by 8, `x<<3`

#### Example 0:
```c
   int x = 8;
   x >>= 2; //x=x>>2 moving right by 2 bits = divide by 4
   printf("%d",x);
```
```
Output:
2
```
# Control Statements and Loops

## Switch Statement
The switch statement compares the value of a given variable (or expression)  against a list of case values and when a match is found, a block of statements associated with that case is executed

```c
switch(variable)
{
    case <value_1>:
        <action>
        break;
    
    case <value_2>:
        <action>
        break;
 

    default:
        <action>
        break;
}
```
## Arrays

### `sizeof()` gives total data stored in array

```c
int main()
{
    int arr[5]={1,2,3,4,5};

    printf("Size of array: %d\n", sizeof(arr));
    printf("Size of element: %d\n", sizeof(arr[0]));
    printf("Length of array: %d\n", sizeof(arr)/sizeof(arr[0]));
}
```
Output
```
Size of array: 20
Size of element: 4
Length of array:5
```

### Memory Allocated Per Datatype:
- integer data type variable is 4 bytes.
- float variable is 4 bytes
- (unsigned) char data type variable is 1 byte
- double data type is 8 bytes
- pointer data type is 8 bytes 

### String and Character:

```c
int main()
{
   char str[5]="ABCDE";
   printf("%s\n", str);

   for(int i=0;i<5;i++)
   {
    printf("%c ", str[i]);
   }
```
```
Output:
ABCDE
A B C D E 
```

## 2D Arrays
```c
int main()
{
    //Get input for a 2D array
    int arr[2][2];

    for(int i=0; i<2;i++)
    {
        for(int j=0; j<2; j++)
        {
            printf("Enter the value of element %d x %d:", i,j);
            scanf("%d", &arr[i][j]);
        }
    }

    //Print a matrix
    for(int i=0; i<2;i++)
    {
        for(int j=0;j<2;j++)
        {
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }

    //Sum up rows:
  
    for(int i=0;i<2;i++)
    {
        int sum=0;
        for(int j=0;j<2;j++)
        {
            sum+= arr[i][j];
        }
        printf("Sum of elements in row %d: %d\n", i, sum);

    }

    //Sum up columns:
    
    for(int i=0;i<2;i++)
    {
        int sum=0;
        for(int j=0;j<2;j++)
        {
            sum+= arr[j][i];
        }
        printf("Sum of elements in column %d: %d\n", i, sum);

    }


   


}
```
```
Output
Enter the value of element 0 x 0:1
Enter the value of element 0 x 1:2
Enter the value of element 1 x 0:3
Enter the value of element 1 x 1:4
1 2 
3 4
Sum of elements in row 0: 3
Sum of elements in row 1: 7
Sum of elements in column 0: 4
Sum of elements in column 1: 6
```

```c
#include <stdio.h>
#include <Math.h>

int main()
{
    int mat[5][5];
    int i,j;

    for(i=0; i<5; i++) //Rows
    {
        printf("Enter student %d marks:\n", i+1);
        for(j=0; j<5; j++) //Columns
        {
            printf("Enter course %d marks", j+1);
            scanf("%d", &mat[i][j]);
        }
    }

    for(i=0; i<5; i++)
    {
        for(j=0; j<5; j++)
        {
            printf("%d  ", mat[i][j]);
        }
        printf("\n");
    }
    
    //Sum all columns:
    for(i=0; i<5; i++)
    {
        int sum = 0;
        printf("Student %d total is: ", i+1);
        for(j=0; j<5; j++)
        {
            sum += mat[i][j];
        }
        printf("Sum: %d\n", sum);
    }
}
```
Output
```
Enter student 1 marks:
Enter course 1 marks1
Enter course 2 marks2
Enter course 3 marks3
Enter course 4 marks4
Enter course 5 marks5
Enter student 2 marks:
Enter course 1 marks1
Enter course 2 marks2
Enter course 3 marks3
Enter course 4 marks4
Enter course 5 marks5
Enter student 3 marks:
Enter course 1 marks1
Enter course 2 marks2
Enter course 3 marks3
Enter course 4 marks4
Enter course 5 marks5
Enter student 4 marks:
Enter course 1 marks1
Enter course 2 marks2
Enter course 3 marks3
Enter course 4 marks4
Enter course 5 marks5
Enter student 5 marks:
Enter course 1 marks1
Enter course 2 marks2
Enter course 3 marks3
Enter course 4 marks4
Enter course 5 marks5
1  2  3  4  5  
1  2  3  4  5
1  2  3  4  5
1  2  3  4  5
1  2  3  4  5
Student 1 total is: Sum: 15
Student 2 total is: Sum: 15
Student 3 total is: Sum: 15
Student 4 total is: Sum: 15
Student 5 total is: Sum: 15

```

# Pointers



## Basic Pointer Declaration and Pointing to a Variable
```c
int var = 50;
    printf("Address of var: %d\n", &var);
   
   //Declare a pointer:
   int *pt;
   pt = &var;

   printf("*pt contains: %d \n", *pt);
   printf("pt contains: %d \n", pt);

```
```
Output:
Address of var: 6291140
*pt contains: 50 
pt contains: 6291140
```

NOTE:
`int *pt = &var;` is equivalent to 
 ```
 int *pt; 
 pt = &var;
 ```

#### You cannot access one datatype variable using different datatype pointer (if you do, you will get 0 when trying to view the variable through that wrong pointer using format specifier)
#### To access a datatype, use THAT datatype pointer

## Typecasting
```c
int main()
{
    int a = 5;
    float b = 1.2;

    void *ptr;
    ptr = &a;
    printf("A is: %d\n", *(int *)ptr);

    ptr = &b;
    printf("B is: %f", *(float *)ptr);

}
```
```
A is: 5
B is: 1.200000
```
- Void pointers can be reused by doing typecasting, so that they align with the datatype of the variable you are pointing to

 ## Changing the value of variable pointed to by a pointer
 To change data inside `var` using pointer `*pt1` which is currently pointing to `var`

 ```c
int var = 50;
printf("Var contains: %d\n", var);

int *pt1 = &var;

//Changing var from 50 to 60
*pt1 = 60;
printf("Var contains: %d", var);
```
```
Output:
Var contains: 50
Var contains: 60
```

 # Strings
 String: array of characters, terminated by a null character (`\0`)

## Initialisation
 ```c
int main()
{
    char str[] = "VIT";
    printf("Size of str: %d", sizeof(str));
    printf("%s", str);
}
 ```

Output
```
Size of str: 4
VIT
```

## Take Input
```c
int main()
{
    char str[max_len];
    scanf("%s", &str);
    printf("\n%s", str);
}
```

# String Functions
## gets()
- Allows user to retrieve a multi-word string which cannot be done by scanf(it returns only first word of sentence)
- `gets(<variable_name>)`

```c
    char str[max_len];
    gets(str);
    printf("U entered: %s", str);
```
Output
```
sneha is here
U entered: sneha is here
```

## puts()

## strlen()
`strlen(<variable_name>)`

```c
int len;
char name[50] = "SNEHA S"; //Length will be SNEHA S length, not the max of 50
len = strlen(name);
```
```
Output: len = 7
```


## strcopy()
`strcopy(<target_var>, <source_var>);`
- copies the source string to target variable



Doubt:
```c

#include <stdio.h>

int main()
{
    char a = 'Hello';

    int size = sizeof(a);
    printf("The size of a is: %d\n", size);
    
    printf("Variable a is: %c", a);
}
```

How is output 'o'?
```
The size of a is: 1
Variable a is: o
```
