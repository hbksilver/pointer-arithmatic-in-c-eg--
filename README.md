# pointer-arithmatic-in-c-eg--
Project 4, IT Program Design
1. (40 points) Note: This program will be graded based on whether the required functionality were
implemented correctly (using pointer arithmetic) instead of whether it produces the correct output,
for the functionality part (80% of the grade).
Modify merge.c (attached, Project 2, #1), the merge function using pointer arithmetic. The function
prototype should be the following. Name your program merge2.c.
void merge(int n, int *a1, int *a2, int *a3);
The function should use pointer arithmetic – not subscripting – to visit array elements. In other words,
eliminate the loop index variables and all use of the [] operator in the function.
2. (60 points) Write a program that allows rearranging of the array elements by slicing the array at a
specified position and put the second part of the array to the beginning of the array and then append the
first part. A sample input/output:
Enter the length of the array: 6
Enter the elements of the array: 3 4 9 8 7 2
Enter the slicing position: 3
Output:
The output array is: 9 8 7 2 3 4
1) Name your program rearrange.c.
2) As part of the solution, write and call the function rearrange() with the following
prototype. The rearrange function should rearrange the array a1 with slicing position s so
that the elements before position s are moved to the end of the elements after position s.
void rearrange(int n, int *a1, int s, int *a2);
The rearrange() function should use pointer arithmetic – not subscripting – to visit array
elements. In other words, eliminate the loop index variables and all use of the [] operator in
the function.
3) In the main function, ask the user to enter the length of the array, declare the array with the
length, read in the values for the array and the slicing position and call the rearrange
function. The main function should display the result.
Before you submit:
1. Compile with –Wall. Be sure it compiles on the student cluster with no errors and no warnings.
gcc -Wall merge2.c
gcc -Wall rearrange.c
2. Be sure your Unix source file is read & write protected. Change Unix file permission on Unix:
chmod 600 merge2.c
chmod 600 rearrange.c
3. Test your program with the shell scripts on Unix:
chmod +x try_merge
./try_merge
chmod +x try_rearrange
./try_rearrange
Total points: 100
1. A program that does not compile will result in a zero.
2. Runtime error and compilation warning 5%
3. Commenting and style 15%
4. Functionality 80%
Problem #1: The function should use pointer arithmetic – not subscripting – to visit array
elements. (80%)
Problem #2: The rearrange () function should use pointer arithmetic – not subscripting – to visit
array elements. (60%)
Programming Style Guidelines
The major purpose of programming style guidelines is to make programs easy to read and understand.
Good programming style helps make it possible for a person knowledgeable in the application area to
quickly read a program and understand how it works.
1. Your program should begin with a comment that briefly summarizes what it does. This comment
should also include your name.
2. In most cases, a function should have a brief comment above its definition describing what it
does. Other than that, comments should be written only needed in order for a reader to
understand what is happening.
3. Information to include in the comment for a function: name of the function, purpose of the
function, meaning of each parameter, description of return value (if any), description of side
effects (if any, such as modifying external variables)
4. Variable names and function names should be sufficiently descriptive that a knowledgeable
reader can easily understand what the variable means and what the function does. If this is not
possible, comments should be added to make the meaning clear.
5. Use consistent indentation to emphasize block structure.
6. Full line comments inside function bodies should conform to the indentation of the code where
they appear.
7. Macro definitions (#define) should be used for defining symbolic names for numeric constants.
For example: #define PI 3.141592
8. Use names of moderate length for variables. Most names should be between 2 and 12 letters
long.
9. Use underscores to make compound names easier to read: tot_vol or total_volumn is
clearer than totalvolumn.


#include <stdio.h>


void merge(int n, int a1[], int a2[], int a3[]);

int main(void)
{
  int i;
  
  int N;
  printf("Please enter the length of the input array: ");
  scanf("%d", &N);

  int a[N];
  int a1[N];
  int b[2*N];
  

  printf("Enter %d numbers for the first array: ", N);
  for (i = 0; i < N; i++)
    scanf("%d", &a[i]);

 printf("Enter %d numbers for the second array: ", N);
  for (i = 0; i < N; i++)
    scanf("%d", &a1[i]);


  merge(N, a, a1, b);

  printf("Output array:");
  for (i = 0; i < 2*N; i++)
    printf(" %d", b[i]);
  printf("\n");

  return 0;
}

void merge(int n, int a1[], int a2[],int a3[])
{
	int i, j = 0;
	for(i = 0; i < n; i++, j+=2){
	   a3[j]= a1[i];
	   a3[j+1] = a2[i];
	}
}    



# Written by Jing Wang for Program Design
# try_merge is a Unix shell script that will be used to test project 2.
# To use the script, copy it into the same directory as your scource file
# Set execute permission for the file by issuing the command:
# chmod +x try_merge
# Compile your program, producing a.out as the executable
# To run the script, type 
# ./try_merge
# The user input from the script will not be shown on the screen.
# Compare the results from your program with the expected results on the test cases.
echo '===================================================='
./a.out <<-EndOfInput
5
3 9 1 -4 8
1 2 4 5 7
EndOfInput
echo '----------------------------------------------------'
echo 'Expected:'
echo 'Enter the length of the input array: 5'
echo 'Enter the first array elements: 3 9 1 -4 8'
echo 'Enter the second array elements: 1 2 4 5 7'
echo 'Output array: 3 1 9 2 1 4 -4 5 8 7'
echo '===================================================='
./a.out <<-EndOfInput
3
-9 0 1
8 7 2
EndOfInput
echo '----------------------------------------------------'
echo 'Expected:'
echo 'Enter the length of the input array: 3'
echo 'Enter the first array elements: -9 0 1'
echo 'Enter the second array elements: 8 7 2'
echo 'Output array: -9 8 0 7 1 2'
echo '===================================================='


# Written by Jing Wang for IT Program Design
# try_rearrange is a Unix shell script that will be used to test project 4.
# To use the script, copy it into the same directory as your scource file
# Set execute permission for the file by issuing the command:
# chmod +x try_rearrange
# Compile your program, producing a.out as the executable
# To run the script, type 
# ./try_rearrange
# The user input from the script will not be shown on the screen.
# Compare the results from your program with the expected results on the test cases.
echo '===================================================='
./a.out <<-EndOfInput
5
3 9 1 -4 8
4
EndOfInput
echo '----------------------------------------------------'
echo 'Expected:'
echo 'Enter the length of the input array: 5'
echo 'Enter the array elements: 3 9 1 -4 8'
echo 'Enter the slicing position: 4'
echo 'Output array: -4 8 3 9 1'
echo '===================================================='
./a.out <<-EndOfInput
7
-9 0 1 7 6 3 2
3
EndOfInput
echo '----------------------------------------------------'
echo 'Expected:'
echo 'Enter the length of the input array: 3'
echo 'Enter the first array elements: -9 0 1 7 6 3 2'
echo 'Output array: 1 7 6 3 2 -9 0'
echo '===================================================='

//merge.c stores inputs into 2 arrays and then add them in a third array using a function by Hassan Baraka 
#include <stdio.h>
 
//declare the function merge
void merge(int n, int *a1, int *a2,  int *a3);
 
int main() {
  int a_1[100], a_2[100], length, element_a_1 = 0, element_a_2 = 0, a_3[200], element_a_3;

 // revieve length of the two arrays
  printf("Enter the length of the array: ");
  scanf("%d", &length);

 // recieve elements of array one
  printf("Enter the elements of the fisrt %d array: ", element_a_1);
  for (element_a_1 = 0; element_a_1 < length; element_a_1++) {
    scanf("%d", &a_1[element_a_1]);
  }
 
  // recieve elements of array 2
 
  printf("Enter the elements of the second %d array: ", element_a_2);
  for (element_a_2 = 0; element_a_2 < length; element_a_2++) {
    scanf("%d", &a_2[element_a_2]);
  }

// call function 
  
 merge(length, a_1, a_2, a_3);
   
    //Prints the merged array
    printf("\nMerged array: ");
    for(element_a_3=0; element_a_3<length*2; element_a_3++)
    {
        printf("\t%d\t", a_3[element_a_3]);
    }
  return 0;
}
 
// function definition
void merge(int n, int *a1, int *a2, int *a3)
// merge the two arrays
{ 
int *p_1, *p_2, *p_3;  
for(p_3 = &a3[0], p_1 = &a1[0], p_2 = &a2[0]; p_3< &a3[n*2]; p_3++)
{
    while(p_1 < &a1[n])
    {
       *p_3 = *p_1;
        p_3++;
  p_1++;
    }
    while(p_2 < &a2[n])
    {
        *p_3 = *p_2;
        p_3++;
        p_2++;
    }
 }

}


//rearrange.c rearranges array elements when user enter the slicing point s, written by Hassan Baraka
 #include<stdio.h>

//rearrange function prototype
void rearrange(int n, int *a1, int s, int *a2);

int main(void)
{

int length, a1[50], slice = 0, a2[50], element_a_1 = 0, element_a_2 = 0;

// enter length of array
printf("Please provide length of the array: ");
scanf("%d", &length);

// enter array elements
 printf("Enter the elements of %d array: ", element_a_1);
  for (element_a_1 = 0; element_a_1 < length; element_a_1++) {
    scanf("%d", &a1[element_a_1]);
  }

//Enter slicing point
printf("Please enter slicing point: ");
scanf("%d", &slice);

// call rearrange function
rearrange(length, a1, slice, a2);

// print rearanged array
printf("\n rearranged array is: ");
for(element_a_2=0; element_a_2<length; element_a_2++)
    {
        printf("\t%d\t", a2[element_a_2]);
    }
  return 0;
}

// rearrange function
void rearrange(int n, int *a1, int s, int *a2)
{
// slice array1
int *p1, *p2;
for(p1 = a1+s-1, p2 = a2; p2 < a2+n; p2++)
{
while(p1 < &a1[n])
{
*p2 = *p1;
p2++;
p1++;
}
}
for(p1 = a1, p2 = a2+s; p2 < a2+n; p2++)
{
while(p1 < &a1[s])
{
*p2 = *p1;
p2++;
p1++;
}
}
}


