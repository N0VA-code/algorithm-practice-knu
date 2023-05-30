```txt
Time Complexity Analysis 1
Description
Analyze the following program and print the output value according to the input value.
However, as running the code as it is will lead to a timeout, you should compute the time complexity of the fun() function and directly print the result.
cpp
Copy code
#include <bits/stdc++.h>
using namespace std;

typedef long long long_t;

long_t fun(long_t n) {
    long_t i, j, cnt = 0;
    for (i=1; i<=4*n; i+=2)
        for (j=n; j>=1; j--)
            cnt++;
    return cnt;
}

int main() {
    long_t n;
    scanf("%lld", &n);
    printf("%lld", fun(n));
}
Input
The first line gives the value of the input parameter N.
Output
The first line prints the output value according to the value of N.
Sample Input 1
1
Sample Output 1
2
Sample Input 2
4
Sample Output 2
32
Sample Input 3
1024
Sample Output 3
2097152
```

```cpp
#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

typedef long long long_t;

long_t fun(long_t n) {

    return 2*n*n;
}

int main() {
    long_t n;
    scanf("%lld", &n);
    printf("%lld", fun(n));
}

```

```txt
Time Complexity Analysis 2
Description
This problem is the same as problem 1.
cpp
Copy code
#include <bits/stdc++.h>
using namespace std;

typedef long long long_t;

long_t fun(long_t n, long_t m, long_t p) {
    long_t i, j, k, cnt = 0;
    for (i=1; i<=2*n; i+=4)
        for (j=1; j<=2*m; j*=2)
            for (k=4*p; k>=1; k/=2)
                cnt++;
    return cnt;
}

int main() {
    long_t n, m, p;
    scanf("%lld %lld %lld", &n, &m, &p);
    printf("%lld", fun(n, m, p));
}
Input
The first line gives the input values N, M, and P in order.
Output
The first line prints the output of the above program.
Sample Input 1
1 2 4
Sample Output 1
15
Sample Input 2
4 8 16
Sample Output 2
70
Sample Input 3
1024 2048 4096
Sample Output 3
99840
```

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef long long long_t;

long_t fun(long_t n, long_t m, long_t p) {
    long_t i, j, k, cnt = 0;
    for (i=1; i<=2*n; i+=4)
        for (j=1; j<=2*m; j*=2)
            for (k=4*p; k>=1; k/=2)
                cnt++;
    return cnt;
}

int main() {
    long_t n, m, p;
    scanf("%lld %lld %lld", &n, &m, &p);
    printf("%lld", fun(n, m, p));
}

```

```txt
Time Complexity Analysis 3
Description
This problem is the same as problem 1.
cpp
Copy code
#include <bits/stdc++.h>
using namespace std;

typedef long long long_t;

long_t fun(long_t n) {
    if (n == 0)
        return 1;
    else
        return fun(n/2) + fun(n/2) + fun(n/2) + fun(n/2);
}

int main() {
    long_t n;
    scanf("%lld", &n);
    printf("%lld", fun(n));
}
Input
The first line gives the input value.
Output
The first line prints the output value.
Sample Input 1
1
Sample Output 1
4
Sample Input 2
4
Sample Output 2
64
Sample Input 3
1024
Sample Output 3
4194304
```

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef long long long_t;

long_t fun(long_t n) {
   return pow(2*n,2);
}

int main() {
    long_t n;
    scanf("%lld", &n);
    printf("%lld", fun(n));
} 

```

```txt
Time Complexity Analysis 4
Description
This problem is the same as the previous problem.
cpp
Copy code
#include <bits/stdc++.h>
using namespace std;

typedef long long long_t;

long_t fun(long_t n) {
    if (n == 0)
        return 1;
    else {
        long_t s = 0;
        for (int i=1; i<=8; i++)
            s += fun(n/4);
        return s;
    }
}

int main() {
    long_t n;
    scanf("%lld", &n);
    printf("%lld", fun(n));
}
Input
The first line gives the input value.
Output
The first line prints the output value.
Sample Input 1
1
Sample Output 1
8
Sample Input 2
4
Sample Output 2
64
Sample Input 3
1024
Sample Output 3
262144
```

```cpp
#pragma warning(disable:4996)
#pragma warning(disable:6031)

#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

typedef long long long_t;

int main() {
    long_t n;
    long_t cnt = 0;
    scanf("%lld", &n);
    while (n != 0) {
        cnt++;
        n /= 4;
    }

    printf("%.0f\n", pow(8, cnt));

    return 0;
}
```

```txt
Print Collatz Sequence
Description
According to the Collatz Conjecture proposed by Lothar Collatz in 1937, for all positive integers n, if you repeatedly perform the following operations, it will inevitably converge to 1.
• If n is even, divide n by 2.
• If n is odd, multiply n by 3 and add 1.
The Collatz conjecture remains a famous unsolved problem in mathematics, and it is said that no one has yet been able to prove it.
For a positive integer N, let's call the sequence of numbers that come out when repeating the above operations until N converges to 1 as the Collatz sequence.
Given an arbitrary positive integer N, print the Collatz sequence.
Input
The first line gives a positive integer N.
Output
The first line prints the Collatz sequence for the positive integer N in order.
Sample Input 1
1
Sample Output 1
1
Sample Input 2
7
Sample Output 2
7 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1
Sample Input 3
10
Sample Output 3
10 5 16 8 4 2 1
```

```cpp
#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

typedef long long long_t;

long_t collatz(long_t n)
{
    if (n == 1)
    {
        printf("%d ", n);
        return 1;
    }
    else if (n % 2 == 0)
    {
        printf("%d ", n);
        n=n / 2;
        return collatz(n);
    }
    else
    {
        printf("%d ", n);
        n = 3 * n + 1;
        return collatz(n);
    }
}
int main() {
    long_t n;
    scanf("%lld", &n);
    collatz(n);
}
```

```txt
Longest Collatz Sequence
Description
Given two arbitrary positive integers N and M, find the number K whose Collatz sequence is the longest among the positive integers greater than or equal to N and less than or equal to M, and print the length of K's Collatz sequence and the corresponding Collatz sequence.
However, if there are several numbers with the longest length of the Collatz sequence, choose the largest number as K.
Input
The first line gives two positive integers N, M. (N <= M)
Output
On the first line, print the number K, which has the longest Collatz sequence among the numbers greater than or equal to N and less than or equal to M, and the length of K's Collatz sequence.
On the second line, print K's Collatz sequence.
If there are several numbers with the longest length of the Collatz sequence, choose the largest number as K.
Sample Input 1
1 10
Sample Output 1
9 19
9 28 14 7 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1
Sample Input 2
123 1234
Sample Output 2
1161 181
1161 3484 1742 871 2614 1307 3922 1961 5884 2942 1471 4414 2207 6622 3311 9934 4967 14902 7451 22354 11177 33532 16766 8383 25150 12575 37726 18863 56590 28295 84886 42443 127330 63665 190996 95498 47749 143248 71624 35812 17906 8953 26860 13430 6715 20146 10073 30220 15110 7555 22666 11333 34000 17000 8500 4250 2125 6376 3188 1594 797 2392 1196 598 299 898 449 1348 674 337 1012 506 253 760 380 190 95 286 143 430 215 646 323 970 485 1456 728 364 182 91 274 137 412 206 103 310 155 466 233 700 350 175 526 263 790 395 1186 593 1780 890 445 1336 668 334 167 502 251 754 377 1132 566 283 850 425 1276 638 319 958 479 1438 719 2158 1079 3238 1619 4858 2429 7288 3644 1822 911 2734 1367 4102 2051 6154 3077 9232 4616 2308 1154 577 1732 866 433 1300 650 325 976 488 244 122 61 184 92 46 23 70 35 106 53 160 80 40 20 10 5 16 8 4 2 1
```

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

typedef long long long_t;

long_t collatz(long_t n, int& rep)
{
    rep++;
    if (n == 1)
    {
       // printf("%d ", n);
        return rep;
    }
    else if (n % 2 == 0)
    {
       // printf("%d ", n);
        n = n / 2;
        return collatz(n,rep);
    }
    else
    {
        //printf("%d ", n);
        n = 3 * n + 1;
        return collatz(n,rep);
    }
}

long_t print_collatz(long_t n)
{
    if (n == 1)
    {
        printf("%d ", n);
        return 1;
    }
    else if (n % 2 == 0)
    {
        printf("%d ", n);
        n = n / 2;
        return print_collatz(n);
    }
    else
    {
        printf("%d ", n);
        n = 3 * n + 1;
        return print_collatz(n);
    }
}

int main() {
    long_t n,m,max=0,idx=0;
    int i,rep = 0;
    scanf("%lld %lld", &n, &m);
    long_t save = n;
    long_t k = m - n + 1;
    long_t* arr = new long_t[k];
    for (i = 0; i < k; i++)
    {
        arr[i] = collatz(n, rep);
        rep = 0;
        n++;
    }
    for (i = 0; i < k; i++)
    {
        if (arr[i] > max)
        {
            max = arr[i];
            idx = i+1;
        }
    }

    printf("%lld %lld\n",(idx+save-1),(max-1));
    print_collatz(idx+save-1);
}
```

```txt
Tower of Hanoi
Description
In the Tower of Hanoi, there are three pillars and N disks of different sizes. Let's call the three pillars A, B, and C, and initially, all the disks are on pillar A. The monks of the Hanoi tower must move all the disks on pillar A to pillar C. The rules for moving the disks are as follows:
• Only one disk can be moved at a time, and the disk on the top of each pillar must be moved.
• A smaller disk must always be placed on a larger disk.
A disk movement is indicated by the name of the start pillar and the destination pillar of the disk to be moved. For example, moving one disk from pillar A to pillar C is indicated as follows:
A -> B
Junyeon wrote a program using the following recursive algorithm to solve this problem.
cpp
Copy code
#include <bits/stdc++.h>
using namespace std;

void hanoi(int n, char src, char via, char dst) {
    if (n == 1) {
        printf("%c -> %c\n", src, dst);
    }
    else {
        hanoi(n-1, src, dst, via);
        hanoi(1, src, via, dst);
        hanoi(n-1, via, src, dst);
    }
}

int main() {
    int n;
    cin >> n;
    hanoi(n, 'A', 'B', 'C');
}
When the number of disks N and the movement number K are given, print the start pillar and the destination pillar of the disk moving for the K-th time when moving N disks using the above algorithm.
Input
The first line gives the number of disks N and the movement number K.
Output
The first line prints the start pillar and the destination pillar of the disk moving for the K-th time.
The second line prints the total number of calls to the hanoi() function.
Sample Input 1
3 4
Sample Output 1
A -> C
10
Sample Input 2
4 8
Sample Output 2
A -> C
22
Sample Input 3
10 10
Sample Output 3
B -> A
1534
```

```cpp
#include <cmath>
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

void hanoi(int n, char src, char via, char dst,int &cnt, int find, int &rep) {
   
    if (n ==1 &&cnt == find)
    {
        printf("%c -> %c\n", src, dst);
    }

   if (n == 1) {
        cnt++;
    }
    else {
       rep++; hanoi(n - 1, src, dst, via, cnt, find, rep);
       rep++; hanoi(1, src, via, dst, cnt, find, rep);
       rep++; hanoi(n - 1, via, src, dst, cnt, find, rep);
    }

}

int main() {
    int n, find, cnt = 1, rep = 1;
    scanf("%d %d", &n, &find);
    hanoi(n, 'A', 'B', 'C',cnt,find,rep);
    printf("%d", rep);
    return 0;
} 
```
