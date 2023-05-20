```txt
These codes and overall same lower codes under this respiratory are KNU Algorithm practice subaject's solutions,

All codes are written by me(N0VA-code)
```

```txt
AP1-1
Sequential Search
Description
Please implement Algorithm 1.1. Sequential Search from the textbook as follows in C++ language.
cpp
Copy code
#include <bits/stdc++.h>
using namespace std;

void seqsearch(int n, vector<int> S, int x, int& location);

int main() {
    int n, m;
    scanf("%d %d", &n, &m);
    vector<int> S(n+1);
    for (int i = 1; i <= n; i++)
        scanf("%d", &S[i]);
    while (m--) {
        int x, location;
        scanf("%d", &x);
        seqsearch(n, S, x, location);
        if (location > 0)
            printf("%d is in %d.\n", x, location);
        else
            printf("%d is not in S.\n", x);
    }
}
When submitting to the online judge, only the implementation of the seqsearch() function needs to be submitted.
Input
The first line provides two positive integers N and M.
The second line provides N positive integers.
The third line provides M positive integers.
Output
From the first line, one line at a time, for the positive integer x given in the third line of the input, the location is printed in the following format.
xx is in locationlocation.
If xx does not exist in the given input, it is printed as follows.
xx is not in S.
Sample Input 1
6 3
10 7 11 5 13 8
5 8 3
Sample Output 1
5 is in 4.
8 is in 6.
3 is not in S.
```

```cpp
void seqsearch(int n, vector<int> S, int x, int& location)

{

    location = 1;

    while (location <= n && S[location] != x)

    {

       location++;

    }

    

    if (location > n) location = 0;

}
```
```txt
AP1-2
Adding Array Elements
Description
Please implement Algorithm 1.2. Adding Array Members from the textbook as follows in C++ language.
cpp
Copy code
#include <bits/stdc++.h>
using namespace std;

int sum(int n, vector<int> S);

int main() {
    int n;
    scanf("%d", &n);
    vector<int> S(n+1);
    for (int i = 1; i <= n; i++)
        scanf("%d", &S[i]);
    printf("%d", sum(n, S));
}
When submitting to the online judge, only the implementation of the sum() function needs to be submitted.
Input
The first line provides a positive integer N.
The second line provides N array elements.
Output
The first line prints the sum S of the array elements.
Sample Input 1
6
10 7 11 5 13 8
Sample Output 1
54
```

```cpp
int sum(int n, vector<int> S) {

    int m = 0;

    for(int i=1;i<n+1;i++)

    {

        m = m + S[i];

    }



    return m;

}
```
```txt
AP1-3
Exchange Sort
Description
Implement the Exchange Sort algorithm in C++ as follows:
#include <bits/stdc++.h>
using namespace std;
void exchange(int n, vector<int>& S);
int main() {
int n;
scanf("%d", &n);
vector<int> S(n+1);
for (int i = 1; i <= n; i++)
scanf("%d", &S[i]);
exchange(n, S);
for (int i = 1; i <= n; i++)
if (i < n)
printf("%d ", S[i]);
else
printf("%d\n", S[i]);
}
For online judge submission, only the implementation part of the exchange() function needs to be submitted.
Input
The first line contains a positive integer N.
The second line contains N positive integers.
Output
Print the array S in ascending order on a single line.
Sample Input 1
6
10 7 11 5 13 8
Sample Output 1
5 7 8 10 11 13
```
```cpp
void exchange(int n, vector<int>& S)

{

    int cnt = 1;

    while (cnt != 0)

    {

        int cnt = 0;

        for (int i = 1; i < n; i++)
        {

            if (S[i] > S[i + 1])

            {

                swap(S[i], S[i + 1]);

                cnt++;

            }

        }

        if (cnt == 0) break;

    }



    return;

}
```
```txt
AP 1-4
Matrix Multiplication
Description
Implement Algorithm 1.4 Matrix Multiplication from the textbook in C++ language as follows.
cpp
Copy code
#include <bits/stdc++.h>
using namespace std;

typedef vector<vector<int>> matrix_t;

void matrixmult(int n, matrix_t A, matrix_t B, matrix_t& C);

void matrixread(int n, matrix_t& M) {
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            scanf("%d", &M[i][j]);
}

int main() {
    int n;
    scanf("%d", &n);

    matrix_t A(n+1, vector<int>(n+1));
    matrixread(n, A);
    matrix_t B(n+1, vector<int>(n+1));
    matrixread(n, B);
    matrix_t C(n+1, vector<int>(n+1));
    matrixmult(n, A, B, C);

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            if (j < n)
                printf("%d ", C[i][j]);
            else
                printf("%d\n", C[i][j]);
        }
    }
}
When submitting online, only the implementation part of the matrixmult() function needs to be submitted.
Input
The first line contains a positive integer N.
The next N lines contain the elements of the first NN matrix, with one row per line.
The following N lines contain the elements of the second NN matrix, with one row per line.
Output
Print the result of the matrix multiplication as N lines, with one row per line.
Sample Input 1
2
2 3
4 1
5 7
6 8
Sample Output 1
28 38
26 36
```
```cpp
for (i = 1; i <= n; i++) {
    for (j = 1; j <= n; j++) {
        C[i][j] = 0;
        for (k = 1; k <= n; k++) {
            C[i][j] = C[i][j] + A[i][k] * B[k][j];
        }
    }
}

```
```txt
AP1-5
Binary Search
Description
Implement the Binary Search algorithm in C++ as follows:
#include <bits/stdc++.h>
using namespace std;
void binsearch(int n, vector<int> S, int x, int& location);
int main() {
int n, m;
scanf("%d %d", &n, &m);
vector<int> S(n+1);
for (int i = 1; i <= n; i++)
scanf("%d", &S[i]);
sort(S.begin() + 1, S.end());
while (m--) {
int x, location;
scanf("%d", &x);
binsearch(n, S, x, location);
if (location > 0)
printf("%d is in %d.\n", x, location);
else
printf("%d is not in S.\n", x);
}
}
For online judge submission, only the implementation part of the binsearch() function needs to be submitted.
Input
The first line contains two positive integers N and M.
The second line contains N positive integers.
The third line contains M positive integers.
Output
Print the positions of the given positive integers (x) from the third line of the input as follows:
xx is in locationlocation.
If xx does not exist in the given input, print the following:
xx is not in S.
Sample Input 1
6 3
10 7 11 5 13 8
5 8 3
Sample Output 1
5 is in 1.
8 is in 3.
3 is not in S.
```
```cpp
void binsearch(int n, vector<int> S, int x, int& location)

{

    int start =1, end = n;

    location = 0;

    while (start <= end)

    {

        int mid = (start + end) / 2;

        if (x < S[mid])

        {

           end = mid-1;

        }

        else if (x > S[mid])

        {

            start = mid + 1;

        }

        else

        {

            location = mid;

            break;

        }

    }

}

```
```txt
AP1-6
Fibonacci Numbers (Recursive)
Description
Implement the recursive version of the Fibonacci algorithm, Algorithm 1.6 Fibonacci (Recursive), as follows:
In this problem, along with the Fibonacci number, you should also output the number of times the fib() function is called. To ensure that the Fibonacci numbers do not exceed the range of integers, define the Fibonacci sequence as follows:
F(n) = (F(n-1) + F(n-2)) % 1000000
You can solve this problem in C/C++/Java/Python.
Input
The first line contains a non-negative integer N. (0 <= N <= 300)
Output
Print the Fibonacci number modulo 1000000 on the first line.
Print the number of times the fib() function is called on the second line.
Sample Input 1
0
Sample Output 1
0
1
Sample Input 2
1
Sample Output 2
1
1
Sample Input 3
2
Sample Output 3
1
3
```
```cpp
#pragma warning(disable:4996)
#pragma warning(disable:6031)

#include <iostream>

#include <vector>

#include <algorithm>

using namespace std;

int fib(int n, int& cnt)

{

    cnt++;

    if (n == 0)

    {

        return 0;

    }

    else if (n == 1)

    {

        return 1;

    }

    else

    {

        return ((fib(n - 1, cnt) + fib(n - 2, cnt)) % 1000000);

    }

}

int main(void)

{

    int n;

    int cnt = 0;

    int x;


    scanf("%d", &n);

    x=fib(n, cnt);


    printf("%d\n%d\n", x, cnt);



    return 0;

}
```
```txt
AP1-7
Fibonacci Numbers (Iterative)
Description
Implement the iterative version of the Fibonacci algorithm, Algorithm 1.7 Fibonacci (Iterative), as follows:
To ensure that the Fibonacci numbers do not exceed the range of integers, define the Fibonacci sequence as follows:
F(n) = (F(n-1) + F(n-2)) % 1000000
Input
The first line contains a non-negative integer N. (0 <= N <= 100000)
Output
Print the Fibonacci number modulo 1000000.
Sample Input 1
100
Sample Output 1
915075
Sample Input 2
1000
Sample Output 2
228875
```
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;


int main(void)
{
	int n, x;

	scanf("%d", &n);
	int i;
	int* fibo = new int[n+1];

	fibo[0] = 0;
	if (n > 0)
	{
		fibo[1] = 1;
		for (i = 2; i <= n; i++)
		{
			fibo[i] = ((fibo[i - 1] + fibo[i - 2]) % 1000000);
		}
	}
	printf("%d\n", fibo[n]);

	return 0;
}
```

```txt
AP1-8
Minimum, Median, Maximum
Description
You are given an array of integers. Find and print the minimum, median, and maximum values of the array.
Assume that the array has indices ranging from 1 to N. The median is defined as the value at the ⌈N/2⌉ or ⌈(2N)/2⌉ position, depending on whether N is odd or even.
You can use the sorting library functions provided by your chosen programming language:
C: qsort()
C++: sort()
Java: Arrays.sort() or Collections.sort()
Python: sort() method for lists or sorted() function
Input
The first line contains a positive integer N.
The second line contains N positive integers, representing the elements of the array.
Output
Print the minimum, median, and maximum values on a single line, separated by spaces.
Assume that the array has indices ranging from 1 to N. The median is defined as the value at the ⌈N/2⌉ or ⌈(2N)/2⌉ position, depending on whether N is odd or even.
Sample Input 1
6
10 7 11 5 13 8
Sample Output 1
5 8 13
```

```cpp
#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main(void)
{
	int n,i,m,mid;
	scanf("%d", &n);
	int* arr = new int[n+1];
	for (i = 1; i <= n; i++)
	{
		scanf("%d", &m);
		arr[i] = m;
	}
	sort(arr + 1, arr + n + 1);
	mid = ceil((n+1)/2);
	printf("%d %d %d", arr[1], arr[mid], arr[n]);
}
```
