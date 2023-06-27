```txt
Strassen's Matrix Multiplication Algorithm
Description:
Referencing the textbook and lecture material, implement Algorithm 2.8, Strassen's matrix multiplication algorithm. 
The input to this problem is the value of n and threshold, and two square matrices of size n×n.
Implement Algorithm 2.8 and output the number of calls to the strassen() function and the product of the two square matrices, A×B.
Please note that if the value of n is not a power of 2, you need to redefine n to the nearest power of 2 greater than n.
For example, if you want to find a power of 2, k, greater than n, you can use the following snippet of code:

int k = 1;
while (k < n) k *= 2;
Also, once you've found a power of 2, k, you need to convert the n×n matrix into a k×k matrix (initializing any additional elements to 0).

Input:
The first line provides n and threshold.
From the second line, two n×n matrices are given, with each row on a separate line.

Output:
On the first line, print the number of calls to the strassen() function.
From the second line, print the product of the two matrices, with each row on a separate line.
Note: Be careful not to print a trailing space at the end of each row when printing the matrix.

Sample Input 1 
2 1
2 3
4 1
5 7
6 8
Sample Output 1
8
28 38
26 36
Sample Input 2 
2 2
2 3
4 1
5 7
6 8
Sample Output 2
1
28 38
26 36
Sample Input 3 
5 2
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
Sample Output 3
57
5 5 5 5 5
5 5 5 5 5
5 5 5 5 5
5 5 5 5 5
5 5 5 5 5

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



void print_matrix(int n, matrix_t M);//구현 완
void resize(int n, matrix_t& mat);//구현 완
void madd(int n, matrix_t A, matrix_t B, matrix_t& C);//구현 완
void msub(int n, matrix_t A, matrix_t B, matrix_t& C);//구현 완
void mmult(int n, matrix_t A, matrix_t B, matrix_t& C);//구현 완
void partition(int m, matrix_t M, matrix_t& M11, matrix_t& M12, matrix_t& M21, matrix_t& M22);//구현 완
void combine(int m, matrix_t& M, matrix_t M11, matrix_t M12, matrix_t M21, matrix_t M22);
void strassen(int n, matrix_t A, matrix_t B, matrix_t& C,int threshold,int& cnt);//구현 완

int main(void) {
	int n, threshold,i,j,idx,cnt=0;
	scanf("%d %d", &n, &threshold);
	int k = 1;
	while(k < n){ k *= 2; }
	

	matrix_t A(k+1, vector<int>(k+1));
	for (i = 1; i <= k; i++)
	{
		for (j = 1; j <= k; j++)
		{
			A[i][j] = 0;
		}
	}
	for (i = 1; i <= n; i++)
	{
		for (j = 1; j <= n; j++)
		{
			scanf("%d", &idx);
			A[i][j] = idx;
		}
	}

	matrix_t B(k+1, vector<int>(k+1));
	for (i = 1; i <= k; i++)
	{
		for (j = 1; j <= k; j++)
		{
			B[i][j] = 0;
		}
	}
	for (i = 1; i <= n; i++)
	{
		for (j = 1; j <= n; j++)
		{
			scanf("%d", &idx);
			B[i][j] = idx;
		}
	}

	matrix_t C(k + 1, vector<int>(k + 1));

	strassen(k,A,B,C,threshold,cnt);
	printf("%d\n",cnt);
	print_matrix(n, C);

	return 0;
}

void partition(int m, matrix_t M, matrix_t& M11, matrix_t& M12, matrix_t& M21, matrix_t& M22) {
	for (int i = 1; i <= m; i++)
		for (int j = 1; j <= m; j++) {
			M11[i][j] = M[i][j];
			M12[i][j] = M[i][j + m]; 
			M21[i][j] = M[i + m][j]; 
			M22[i][j] = M[i + m][j + m];
		}
}

void combine(int m, matrix_t& M, matrix_t M11, matrix_t M12, matrix_t M21, matrix_t M22){
	for (int i = 1; i <= m; i++)
		for (int j = 1; j <= m; j++) {
			M[i][j] = M11[i][j];
			M[i][j+m] = M12[i][j];
			M[i+m][j] = M21[i][j];
			M[i+m][j+m] = M22[i][j];
		}
}

void strassen(int n, matrix_t A, matrix_t B, matrix_t& C,int threshold, int& cnt) {
	cnt++;
	matrix_t A11, A12, A21, A22;
	matrix_t B11, B12, B21, B22;
	matrix_t C11, C12, C21, C22;
	matrix_t M1, M2, M3, M4, M5, M6, M7;
	matrix_t L, R;

	if (n <= threshold) {
		mmult(n, A, B, C);
	}
	else {
		// Define local variables here.
		int m = n / 2;
		resize(m, A11); resize(m, A12); resize(m, A21); resize(m, A22);
		resize(m, B11); resize(m, B12); resize(m, B21); resize(m, B22);
		resize(m, C11); resize(m, C12); resize(m, C21); resize(m, C22);
		resize(m, C11); resize(m, C12); resize(m, C21); resize(m, C22);
		resize(m, M1); resize(m, M2); resize(m, M3); resize(m, M4); resize(m, M5);
		resize(m, M6); resize(m, M7); resize(m, L); resize(m, R);

		partition(m, A, A11, A12, A21, A22);
		partition(m, B, B11, B12, B21, B22);
		// Implement Strassen's Method Here.
		madd(m, A11, A22, L); madd(m, B11, B22, R); strassen(m, L, R, M1,threshold,cnt);//m1
		madd(m, A21, A22, L); strassen(m, L, B11, M2,threshold,cnt);//m2
		msub(m, B12, B22, R); strassen(m, A11, R, M3, threshold,cnt);//m3
		msub(m, B21, B11, R); strassen(m, A22, R, M4, threshold,cnt);//m4
		madd(m, A11, A12, L); strassen(m, L, B22, M5, threshold,cnt);//m5
		msub(m, A21, A11, L); madd(m, B11, B12, R); strassen(m, L, R, M6, threshold,cnt);//m6
		msub(m, A12, A22, L); madd(m, B21, B22, R); strassen(m, L, R, M7, threshold,cnt);//m7

		madd(m, M1, M4, L); msub(m, L, M5, R); madd(m, R, M7, C11);//C11
		madd(m, M3, M5, C12);//C12
		madd(m, M2, M4, C21);//C21
		madd(m, M1, M3, L); msub(m, L, M2, R); madd(m, R, M6, C22);//C22

		combine(m, C, C11, C12, C21, C22);
	}
}

void resize(int n, matrix_t& mat)
{
	mat.resize(n + 1, vector<int>(n + 1));
}

void madd(int n, matrix_t A, matrix_t B, matrix_t& C)
{
	int i, j;
	for (i = 1; i <= n; i++)
	{
		for (j = 1; j <= n; j++)
		{
			C[i][j] = A[i][j] + B[i][j];
		}
	}
}

void msub(int n, matrix_t A, matrix_t B, matrix_t& C)
{
	int i, j;
	for (i = 1; i <= n; i++)
	{
		for (j = 1; j <= n; j++)
		{
			C[i][j] = A[i][j] - B[i][j];
		}
	}
}

void mmult(int n, matrix_t A, matrix_t B, matrix_t& C)
{
	int i, j, k;

	for (i = 1; i <= n; i++)
	{
		for (j = 1; j <= n; j++)
		{
			C[i][j] = 0;
			for (k = 1; k <= n; k++)
			{
			        for (j = 1; j <= n; j++)

        {

            C[i][j] = 0;

            for (k = 1; k <= n; k++)

           {

                C[i][j] = C[i][j] + A[i][k] * B[k][j];

            }

        }	C[i][j] = C[i][j] + A[i][k] * B[k][j];
			}
		}
	}
}

void print_matrix(int n, matrix_t M) {
	int i, j, k;

	for (i = 1; i <= n; i++)
	{
		for (j = 1; j <= n; j++)
		{
			if (j == n)
				printf("%d", M[i][j]);
			else
				printf("%d ", M[i][j]);

		}
		printf("\n");
	}
}

```
```txt
Karatsuba Integer Multiplication Algorithm
Description:
Referencing the textbook and lecture material, implement Algorithm 2.9, the Karatsuba integer multiplication algorithm.
This algorithm takes two large integers and a threshold value as input, and outputs the number of calls to the prod() function and the product of the two integers.
Please note that you must remove leading zeros (zeros at the beginning of the number) during the intermediate steps of the algorithm.
You can use the following function to remove leading zeros from a number:

void remove_leading_zeros(LargeInteger& v) {
    while (v.size() != 0 && v.back()==0)
        v.pop_back();
}

Also, note that there may be a significant difference in the number of digits between the two integers being multiplied.
Example: 1000000000000000001 * 111 = 111000000000000000111

Input:
The first line gives the value of threshold.
The second line provides integer A.
The third line provides integer B.

Output:
On the first line, print the number of calls to the prod() function.
On the second line, print the product, C, of A and B.

Sample Input 1 
1
567832
9423723
Sample Output 1
77
5351091478536
Sample Input 2 
1
111111111111111
111111111111111
Sample Output 2
337
12345679012345654320987654321
Sample Input 3 
2
10000000000000000000000000000000000000000001
111
Sample Output 3
25
1110000000000000000000000000000000000000000111
```
```cpp
#pragma warning(disable:4996)
#pragma warning(disable:6031)

#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
#include <sstream>
#include <string>


using namespace std;

typedef vector<int> LargeInteger;


void roundup_carry(LargeInteger& v);
void ladd(LargeInteger a, LargeInteger b, LargeInteger& c);
void lmult(LargeInteger a, LargeInteger b, LargeInteger& c);
void pow_by_exp(LargeInteger u, int m, LargeInteger& v);
void div_by_exp(LargeInteger u, int m, LargeInteger& v);
void rem_by_exp(LargeInteger u, int m, LargeInteger& v);
void prod(LargeInteger u, LargeInteger v, LargeInteger& r,int threshold,int& cnt);
void remove_leading_zeros(LargeInteger& v) {
	while (v.size() != 0 && v.back() == 0)
		v.pop_back();
}

int main() {
	int threshold, idx;
	scanf("%d",&threshold);

	
	int input, cnt=0;

	LargeInteger S;
	char c;
	cin.get(c);

	while (cin.get(c)) {
		if (c == '\n') break;
		int num = c - '0';
		S.push_back(num);
	}

	LargeInteger K;
	while (cin.get(c)) {
		if (c == '\n') break;
		int num = c - '0';
		K.push_back(num);
	}

	LargeInteger res;
	reverse(S.begin(), S.begin() + (S.size()));
	reverse(K.begin(), K.begin() + (K.size()));
	prod(S, K, res,threshold,cnt);
	reverse(res.begin(), res.begin() + (res.size()));
	printf("%d\n", cnt);
	for (int i = 0; i < res.size();i++)
		printf("%d",res[i]);

	return 0;
}

void roundup_carry(LargeInteger& v) {//자리올림 함수
	int carry = 0;
	for (int i = 0; i < v.size(); i++) {
		v[i] += carry;
		carry = v[i] / 10;
		v[i] = v[i] % 10;
	}
	if (carry != 0) v.push_back(carry);
}

void ladd(LargeInteger a, LargeInteger b, LargeInteger& c) {//큰정수 덧셈
	c.resize(max(a.size(), b.size()));
	fill(c.begin(), c.end(), 0);
	for (int i = 0; i < c.size(); i++) {
		if (i < a.size()) c[i] += a[i];
		if (i < b.size()) c[i] += b[i];
	}
	roundup_carry(c);
}

void lmult(LargeInteger a, LargeInteger b, LargeInteger& c) {//큰정수 곱셈
	c.resize(a.size() + b.size() - 1);
	fill(c.begin(), c.end(), 0);
	for (int i = 0; i < a.size(); i++)
		for (int j = 0; j < b.size(); j++) c[i + j] += a[i] * b[j];
	roundup_carry(c);
}

void pow_by_exp(LargeInteger u, int m, LargeInteger& v) {//10의 거듭제곱수로 이동한 결과 벡터저장
	remove_leading_zeros(v);
	if (u.size() == 0)
		v.resize(0);
	else {
		v.resize(u.size() + m);
		fill(v.begin(), v.end(), 0); copy(u.begin(), u.end(), v.begin() + m);
	}
}

void rem_by_exp(LargeInteger u, int m, LargeInteger& v) {//벡터 뒤에 저장
	if (u.size() == 0)
		v.resize(0);
	else { 
		int k = m < u.size() ? m : u.size();//m과u중에 작은거
		v.resize(k);
		copy(u.begin(), u.begin() + k, v.begin());
	}
}

void div_by_exp(LargeInteger u, int m, LargeInteger& v) {//일단 홀수자리 일때 터짐
	if (u.size() == 0)
		v.resize(0);
	else {
		int k = m < u.size() ? m : u.size();
		v.resize(k+1);
		copy(u.begin() + k, u.end(), v.begin()); 
	}
}

void prod(LargeInteger u, LargeInteger v, LargeInteger& r,int threshold,int &cnt) {
	remove_leading_zeros(u); 
	remove_leading_zeros(v); 
	cnt++;
	LargeInteger x, y, w, z;
	LargeInteger t1, t2, t3, t4, t5, t6, t7, t8;
	int n = max(u.size(), v.size());
	if (u.size() == 0 || v.size() == 0) r.resize(0);
	else if (n <= threshold) lmult(u, v, r);
	else {
		int m = n / 2;
		div_by_exp(u, m, x);//u를 10^m으로 나누기 (자릿수 값을 일단 없애야 계산할수 있)
		rem_by_exp(u, m, y);//뒤에 값이니까 모듈러 하면됨 
		div_by_exp(v, m, w);
		rem_by_exp(v, m, z);
		// t2 <- prod(x,w) * 10^(2*m)
		prod(x, w, t1,threshold,cnt); pow_by_exp(t1, 2 * m, t2);
		// t6 <- (prod(x,z)+prod(w,y)) * 10^m
		prod(x, z, t3, threshold,cnt); prod(y, w, t4, threshold,cnt); ladd(t3, t4, t5); pow_by_exp(t5, m, t6);
		// r <- t2 + t6 + prod(y, z)
		prod(y, z, t7, threshold,cnt); ladd(t2, t6, t8); ladd(t7, t8, r);
	}
}
```
```txt
Tromino Puzzle
Description:
Refer to Chapter 2. Exercise 42 (p.94) of the textbook, and solve the tromino puzzle using divide and conquer.
This problem is a typical problem of divide and conquer which divides a problem into four parts and is well known as the tromino tiling problem.
However, in this assignment, the numbers of the tromino tiles are determined in the order in which the trominoes are placed.
For example, in a tromino puzzle like the following, the trominoes are placed in the order shown below.
Input:
The first line will contain three integers, 'n', 'row', and 'col'.
'n' is the size of the n×n tromino puzzle board. (Note: 'n' will always be a power of 2.)
'row' and 'col' are the row and column of the hole in the puzzle, respectively. The values for 'row' and 'col' will be in the range of 0 ≤ 'row', 'col' ≤ n−1.

Output:
Print the board with tile numbers assigned in the order the trominoes are placed. The tile number for the hole is 0.
Be careful not to print a trailing space at the end of each row when outputting the board.

Sample Input 1 
2 0 0
Sample Output 1
0 1
1 1
Sample Input 2 
4 0 0
Sample Output 2
0 2 3 3
2 2 1 3
4 1 1 5
4 4 5 5
Sample Input 3 
8 1 2
Sample Output 3
3 3 4 4 8 8 9 9
3 2 0 4 8 7 7 9
5 2 2 6 10 10 7 11
5 5 6 6 1 10 11 11
13 13 14 1 1 18 19 19
13 12 14 14 18 18 17 19
15 12 12 16 20 17 17 21
15 15 16 16 20 20 21 21
```
```cpp
#pragma warning(disable:4996)
#pragma warning(disable:6031)

#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
#include <sstream>
#include <string>


using namespace std;

typedef vector<vector<int>> Array;

void tromino(Array& arr, int n, int &cnt,int x, int y) {

    if (n == 1) return;

    int m = n / 2;//보드 2분할
    cnt++;
    int i,j;
    int blank1 = 0, blank2 = 0, blank3 = 0,blank4 = 0;
    for (i = x; i < m+x; i++)
    {
        for (j = y; j < m+y; j++)
        {
            if (arr[i][j] != -1)
                blank1++;
            if (arr[i + m][j] != -1)
                blank2++;
            if (arr[i][j+m] != -1)
                blank3++;
            if (arr[i + m][j+m] != -1)
                blank4++;
        }
    }

    if (blank1 % 2 != 0)//첫번째 구멍 있
    {
        arr[m-1+x][m+y] = cnt;
        arr[m +x][m-1+y] = cnt;
        arr[m+x][m+y] = cnt;
    }
    else if (blank2 % 2 != 0)
    {
        arr[m - 1+x][m - 1+y] = cnt;
        arr[m-1+x][m+y] = cnt;
        arr[m+x][m+y] = cnt;
    }
    else if (blank3 % 2 != 0)
    {   
        arr[m - 1+x][m - 1+y] = cnt;
        arr[m +x][m-1+y] = cnt;//이게 문제
        arr[m+x][m+y] = cnt;
    }
    else
    {
        arr[m - 1+x][m - 1+y] = cnt;
        arr[m+x][m - 1+y] = cnt;
        arr[m - 1+x][m+y] = cnt;
    }

    tromino(arr, m,cnt,0+x,0+y);
    tromino(arr, m,cnt,0+x,m+y);
    tromino(arr, m, cnt, m + x, 0 + y);
    tromino(arr, m,cnt,m+x,m+y);
}


    int main(void) {
        int n, a, b,cnt=0;
        scanf("%d %d %d", &n, &a, &b);
        Array arr(n, vector<int>(n,-1));
        arr[a][b] = 0;
        tromino(arr, n, cnt,0,0);
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
            {
                if (j == n - 1)
                    printf("%d", arr[i][j]);
                else
                    printf("%d ", arr[i][j]);
            }
            puts("");
        }
        return 0;
    }


```
