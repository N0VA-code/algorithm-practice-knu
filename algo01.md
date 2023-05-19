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
