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

```
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

```
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

```
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

```
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

```
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

```
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
