```txt
Binary Search (Recursive)
Description
Referring to the textbook and lecture materials, implement Algorithm 2.1 Binary Search (Recursive).
From the list of N integers given in unsorted order, sort the list and then search for M integers,
 outputting the location of the element and the number of calls to the location() function.
Input
The first line provides two positive integers, N and M.
The second line provides N unsorted positive integers.
The third line provides M positive integers to be searched for in the list.
Output
From the first line, output the result of the binary search for each of M lines, one line at a time.
The first value of each line is the number of calls to the location() function during the binary search process.
The second value on each line is the location index in the sorted list (the return value of the location() function).
Sample Input 1 
6 3
10 7 11 5 13 8
5 8 3
Sample Output 1
2 1
1 3
3 0


```

```cpp
#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int binsearch(int *S, int low, int high,int x, int&cnt)
{
	cnt++;
	int mid;

	if (low > high)
	{
		printf("%d ", cnt);
		return -1;
	}
	else {
		mid = (low + high) / 2;
		if (x == S[mid])
		{
			printf("%d ", cnt);
			return mid;
		}
		else if (x < S[mid])
			return binsearch(S,low, mid - 1,x,cnt);
		else
			return binsearch(S,mid + 1, high,x,cnt);
	}
}

int main()
{
	int n,m,find,i,input,cnt=0;
	scanf("%d %d", &n, &m);
	int* S = new int[n+1];
	for (i = 0; i < n; i++)
	{
		scanf("%d",&S[i]);
	}
	sort(S, S + n);

	for (i = 0; i < m; i++)
	{
		scanf("%d", &find);
		printf("%d\n",(binsearch(S, 0, n - 1, find,cnt)+1));
		cnt = 0;
	}
	
}

```

```txt
Merge Sort 1
Description:
Referring to the textbooks and lecture materials, implement the Merge Sort algorithm (Algorithm 2.2/2.3).
Using the merge sort algorithm, sort a list S of N unsorted positive integers in ascending order.
Also, output the total size of additional memory U, V used in the merge() function.
Ignore the size induced by indices, and add only the sizes of h, m for the total sum,
as shown in the following code example. The variable 'cnt' in the code is a global variable used to count the additional memory size.

void mergesort(int n, vector<int>& S) {
    if (n > 1) {
        int h = n / 2, m = n - h;
        vector<int> U(h+1), V(m+1);
        cnt += h + m; // Count additional memory size.
        for (int i = 1; i <= h; i++)
            U[i] = S[i];
        for (int i = h+1; i <= n; i++)
            V[i - h] = S[i];
        mergesort(h, U);
        mergesort(m, V);
        merge(h, m, U, V, S);
    }
}
Input:
The first line gives the number of elements, N, in the list.
The second line provides N unsorted positive integers.
Output:
The first line should output the list sorted in ascending order using merge sort.
The second line should output the total size of additional memory used in the merge() function.
Sample Input 1:
Copy code
8
27 10 12 20 25 13 15 22
Sample Output 1:
Copy code
10 12 13 15 20 22 25 27
24
Sample Input 2:
Copy code
11
91 34 27 66 58 42 37 19 20 73 84
Sample Output 2:
Copy code
19 20 27 34 37 42 58 66 73 84 91
39
```

```cpp
#pragma warning(disable:4996)
#pragma warning(disable:6031)

#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

void merge(int h, int m, vector<int>& U, vector<int>& V, vector<int>& S)
{
	int i = 1, j = 1, k = 1;
	while (i <= h && j <= m) {
		if (U[i] < V[j]) {
			S[k] = U[i];
			i++;
		}
		else {
			S[k] = V[j];
			j++;
		}
		k++;
	}
	if (i > h)
	{
		while (j <= m)
			S[k++] = V[j++];
	}
	else
	{
		while (i <= h)
			S[k++] = U[i++];
	}
}

void mergesort(int n, vector<int>& S, int& cnt) {
	if (n > 1) {
		int h = n / 2, m = n - h;
		vector<int> U(h + 1), V(m + 1);
		cnt += h + m; // 추가 메모리 크기 카운트. cnt는 전역 변수
		for (int i = 1; i <= h; i++)
			U[i] = S[i];
		for (int i = h + 1; i <= n; i++)
			V[i - h] = S[i];
		mergesort(h, U, cnt);
		mergesort(m, V, cnt);
		merge(h, m, U, V, S);
	}
}
int main()
{
    int n, cnt = 0, i, idx = 0;
    scanf("%d", &n);
    vector<int> S(n+1);
    for (i = 1; i <= n; i++)
    {
        scanf("%d", &idx);
        S[i] = idx;
    }
    mergesort(n, S, cnt);
    for (i = 1; i <= n; i++)
    {
      if(i==n)
      {
        printf("%d", S[i]);
      }
      else{
        printf("%d ", S[i]);
      }
    }
    printf("\n%d", cnt);

    return 0;
}

```

```txt
Merge Sort 2
Description:
Referring to the textbooks and lecture materials, implement the Merge Sort 2 algorithm (Algorithm 2.4/2.5).
Using the merge sort 2 algorithm, sort a list S of N unsorted positive integers in ascending order.
Also, output the total number of comparison operations in the merge2() function.
Ignore the comparison operations between indices, and count only the number of comparison operations between elements of list S,
as shown in the following code example.
The variable 'cnt' in the code is a global variable used to count the number of comparison operations.

void merge2(int low, int mid, int high) {
    int i, j, k;
    vector<int> U(high - low + 1);

    i = low; j = mid+1; k = 0;
    while (i <= mid && j <= high) {
        U[k++] = (S[i] < S[j]) ? S[i++] : S[j++];
        cnt++; // Count comparison operations between elements of S. cnt is a global variable
    }

    if (i > mid)
        while (j <= high) U[k++] = S[j++];
    else
        while (i <= mid) U[k++] = S[i++];
    
    for (int t = low; t <= high; t++)
        S[t] = U[t-low];
}
Input:
The first line gives the number of elements, N, in the list.
The second line provides N unsorted positive integers.
Output:
The first line should output the list sorted in ascending order using merge sort 2.
The second line should output the total number of comparison operations in the merge2() function.
Sample Input 1:
Copy code
8
27 10 12 20 25 13 15 22
Sample Output 1:
Copy code
10 12 13 15 20 22 25 27
17
Sample Input 2:
Copy code
11
91 34 27 66 58 42 37 19 20 73 84
Sample Output 2:
Copy code
19 20 27 34 37 42 58 66 73 84 91
26
```

```cpp
#pragma warning(disable:4996)
#pragma warning(disable:6031)

#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;


void merge2(int low, int mid, int high,vector <int>&S,int& cnt) {
	int i, j, k;
	vector<int> U(high - low + 1);

	i = low; j = mid + 1; k = 0;
	while (i <= mid && j <= high) {
		U[k++] = (S[i] < S[j]) ? S[i++] : S[j++];
		cnt++; // S의 원소끼리의 비교 연산 횟수 카운트. cnt는 전역 변수
	}

	if (i > mid)
		while (j <= high) U[k++] = S[j++];
	else
		while (i <= mid) U[k++] = S[i++];

	for (int t = low; t <= high; t++)
		S[t] = U[t - low];
}

void mergesort2(int low, int high, vector <int>& S, int& cnt)
{
	int mid;

	if (low < high) {
		mid = floor((low + high) / 2);
		mergesort2(low, mid,S,cnt);
		mergesort2(mid + 1, high,S,cnt);
		merge2(low, mid, high,S, cnt);
	}
}
int main()
{
	int n, cnt = 0, i, idx = 0;
	scanf("%d", &n);
	vector<int> S(n + 1);
	for (i = 1; i <= n; i++)
	{
		scanf("%d", &idx);
		S[i] = idx;
	}
	mergesort2(1,n, S, cnt);
	for (i = 1; i <= n; i++)
	{
		if (i == n)
		{
			printf("%d", S[i]);
		}
		else {
			printf("%d ", S[i]);
		}
	}
	printf("\n%d", cnt);

	return 0;
}

```
```txt
Quick Sort
Description:
Referring to the textbooks and lecture materials, implement the Quick Sort/Partition algorithm (Algorithm 2.6/2.7). 
Using the quick sort algorithm, sort a list S of N unsorted positive integers in ascending order.
Count and output the number of swap operations executed in the partition() function as shown in the following code example.

void partition(int low, int high, int& pivotpoint) {
    int i, j, pivotitem;

    pivotitem = S[low];
    j = low;
    for (i = low+1; i <= high; i++) {
        if (S[i] < pivotitem) {
            j++;
            swap(S[i], S[j]);
            cnt++; // Count the execution of swap operations.
        }
    }
    pivotpoint = j;
    swap(S[low], S[pivotpoint]);
    cnt++; // Count the execution of swap operations.
}
Input:
The first line gives the number of elements, N, in the list.
The second line provides N unsorted positive integers.
Output:
The first line should output the list sorted in ascending order using quick sort.
The second line should output the total number of swap operations executed.
Sample Input 1 
8
15 22 13 27 12 10 20 25
Sample Output 1
10 12 13 15 20 22 25 27
11
Sample Input 2 
10
1 2 3 4 5 6 7 8 9 10
Sample Output 2
1 2 3 4 5 6 7 8 9 10
9
Sample Input 3 
10
10 9 8 7 6 5 4 3 2 1
Sample Output 3
1 2 3 4 5 6 7 8 9 10
34

```

```cpp
#pragma warning(disable:4996)
#pragma warning(disable:6031)

#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

void partition(int low, int high, int& pivotpoint,int& cnt,vector <int> &S) {
    int i, j, pivotitem;
    pivotitem = S[low];
    j = low;
    for (i = low + 1; i <= high; i++) {
        if (S[i] < pivotitem) {
            j++;
            swap(S[i], S[j]);
            cnt++; // swap 연산의 실행 횟수 카운트
        }
    }
    pivotpoint = j;
    swap(S[low], S[pivotpoint]);
    cnt++; // swap 연산의 실행 횟수 카운트
}

void quicksort(int low, int high, vector<int>&S, int& cnt)
{
    int pivotpoint;

    if (high > low)
    {
        partition(low, high, pivotpoint,cnt,S);
        quicksort(low, pivotpoint - 1, S, cnt);
        quicksort(pivotpoint + 1, high,S,cnt);
    }
}
int main()
{
    int n, cnt = 0, i, idx = 0;
    scanf("%d", &n);
    vector<int> S;
    S.push_back(-99);
    for (i = 1; i <= n; i++)
    {
        scanf("%d", &idx);
        S.push_back(idx);
    }
    quicksort(0,n, S, cnt);
    for (i = 1; i <= n; i++)
    {
      if(i==n){
        printf("%d", S[i]);
      }
      else{
        printf("%d ", S[i]);
      }
    }

    printf("\n%d", cnt-1);

    return 0;
} 

```
```txt
Matrix Exponentiation
Description:
Given an N×N square matrix A and a positive integer b, output the square matrix A^b, which is the b-th power of matrix A.
However, the elements of the matrix should always be the remainder when divided by 1,000 (including during the process of exponentiation).
Note:
This problem involves implementing the modular exponentiation algorithm using the divide and conquer strategy applied to a matrix.
Consider the problem of finding a^b for two integers a and b.
It is clear that if b equals 1, then a should be returned. This is our base case.
Recursive cases can be divided into two conditions:
If b is even, the following rule applies:
a^b = (a^(b/2)) * (a^(b/2))
If b is odd, the following rule applies:
a^b = a * (a^(b/2)) * (a^(b/2))
The following property of modular multiplication can be used in the recursive relationship above:
(a*b) mod N = ((a mod N) * (b mod N)) mod N
After understanding both the base and recursive cases,
we can solve this problem by applying the matrix multiplication algorithm used in previous assignments to the above recursive relationship.
Simple matrix multiplication would require O(b) multiplications, leading to a timeout.
However, using divide and conquer, we can exponentiate in O(log b) multiplications, avoiding a timeout.
Also, we must be careful not to cause overflow during the process by using modular operations.
Input:
The first line gives the size N of the matrix and the size b of the exponent.
From the second line, each of the N elements of the matrix is given for N lines.
Each element of the matrix is a non-negative integer less than 1,000.
Output:
From the first line, output the square matrix A^b, which is the b-th power of matrix A.
During the matrix multiplication process, all elements have the remainder value when divided by 1,000.




Sample Input 1 
2 3
1 2
3 4
Sample Output 1
37 54
81 118
Sample Input 2 
3 1234567
1 2 3
4 5 6
7 8 9
Sample Output 2
432 744 56
958 65 172
484 386 288
```

```cpp
#pragma warning(disable:4996)
#pragma warning(disable:6031)

#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

typedef vector<vector<int>> matrix_t;

matrix_t matrixmult(matrix_t A, matrix_t B)
{
    int n = A.size(), i, j, k;
    matrix_t C(n, vector<int>(n, 0));
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            for (k = 0; k < n; k++) {
                C[i][j] += A[i][k] * B[k][j];
                C[i][j] %= 1000;
            }
        }
    }
    return C;
}

matrix_t matrixpow(matrix_t A, int n) {
    if (n == 1) return A;
    if (n % 2 != 0) {
        matrix_t C = matrixpow(A, n - 1);
        return matrixmult(A, C);
    }
    else {
        matrix_t C = matrixpow(A, floor(n / 2));
        return matrixmult(C, C);
    }
}

int main() {
    int n, m, i, j, idx;
    scanf("%d %d", &n, &m);

    matrix_t A(n, vector<int>(n));
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            scanf("%d", &idx);
            A[i][j] = idx;
            A[i][j] %= 1000;
        }
    }

    matrix_t C = matrixpow(A, m);

    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {
            if (j == n - 1)
            {
                printf("%d", C[i][j]);
            }
            else {
                printf("%d ", C[i][j]);
            }
        }
        puts("");
    }

    return 0;
}
```
