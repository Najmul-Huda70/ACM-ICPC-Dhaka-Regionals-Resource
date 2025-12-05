<details>
    <summary><h1>Binary Exponential Growth in Algorithms</h1></summary>
    Also called: Binary exponentiation or Fast exponentiation
    
```cpp
long long binpow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1) res *= a;   // multiply if the current bit is 1
        a *= a;                // square the base
        b >>= 1;               // shift right (divide by 2)
    }
    return res;
}
```
Use Cases

Modular exponentiation: (𝑎^𝑏)%𝑚

Cryptography (RSA)

Recurrence relations in algorithms (like Fibonacci)
<details>
    
<summary><h2>Problem</h2></summary>

- [Exponentiation](https://cses.fi/problemset/task/1095/)
- [Exponentiation II](https://cses.fi/problemset/task/1712)


</details>
</details>
<details>
    <summary><h1>Matrix Exponential Growth in Algorithms</h1></summary>
Used to compute sequences or recurrences efficiently. Instead of computing each term sequentially, we can represent the recurrence as a matrix multiplication and raise the matrix to a power.

Example: Fibonacci sequence   F(n)=F(n−1)+F(n−2)
```cpp
struct Matrix {
    long long m[2][2];
};

Matrix multiply(Matrix a, Matrix b) {
    Matrix res;
    for(int i=0;i<2;i++)
        for(int j=0;j<2;j++){
            res.m[i][j] = 0;
            for(int k=0;k<2;k++)
                res.m[i][j] += a.m[i][k] * b.m[k][j];
        }
    return res;
}

Matrix binpow(Matrix a, long long n) {
    Matrix res = {{{1,0},{0,1}}}; // identity matrix
    while(n>0) {
        if(n&1) res = multiply(res,a);
        a = multiply(a,a);
        n >>= 1;
    }
    return res;
}
```
Use Cases

Fibonacci & other linear recurrences

Dynamic programming optimization

Graph walks counting (paths of length n)

 <details>
    <summary><h2>Problem</h2></summary>
     
- [Problem - A](#)

</details>
</details>
<details>
    <summary><h1>Modular Arithmetic Function</h1></summary>
    
Modular arithmetic is key in competitive programming and cryptography. Operations are done modulo a number 
𝑚, (a+b)mod m.

<img width="850" height="246" alt="image" src="https://github.com/user-attachments/assets/36c4debb-bd84-4389-bd48-7d1e25cd95d4" />


```cpp
long long modAdd(long long a, long long b, long long m) {
    return (a + b) % m;
}

long long modMul(long long a, long long b, long long m) {
    return (a % m * b % m) % m;
}

long long modPow(long long a, long long b, long long m) {
    long long res = 1;
    a %= m;
    while(b > 0) {
        if(b & 1) res = (res * a) % m;
        a = (a * a) % m;
        b >>= 1;
    }
    return res;
}
```
# Tower of Power mod Problem : 
<img width="733" height="187" alt="image" src="https://github.com/user-attachments/assets/b2771c17-76cf-4414-98c8-012e593489cb" />

```cpp
const int mod = 1e9 + 7;
int modPow(int a, int b, int mod)
{
    int res = 1;
    a %= mod;
    while (b > 0)
    {
        if (b & 1)
            res = (1LL * res * a) % mod;
        a = (1LL * a * a) % mod;
        b >>= 1;
    }
    return res;
}

void solve()
{
    int a, b, c;
    cin >> a >> b >> c;
    // at first find b^c % (mod-1);
    int bPOWc = modPow(b, c, mod - 1);
    // find a^(b^c) % mod ;
    int ans = modPow(a, bPOWc, mod);
    cout << ans << endl;
}
```

<img width="874" height="472" alt="image" src="https://github.com/user-attachments/assets/970b1656-df2b-4ac9-a9ac-17f4f816a1b5" />

```cpp
long long modPow(long long a, long long b, long long p) {
    long long res = 1;
    a %= p;
    while (b > 0) {
        if (b & 1) res = (res * a) % p;
        a = (a * a) % p;
        b >>= 1;
    }
    return res;
}

// Modular inverse using Fermat's little theorem
long long modInverse(long long a, long long p) {
    return modPow(a, p - 2, p); // Only valid if p is prime
}
```
Example Usage
```cpp
int main() {
    long long a = 3, p = 7; // 7 is prime
    cout << modInverse(a, p) << "\n"; // Output: 5, because 3*5 ≡ 1 mod 7
}
```
<img width="764" height="492" alt="Screenshot 2025-12-01 222545" src="https://github.com/user-attachments/assets/afb248bc-26e3-47ff-990e-023fe246ab05" />

<details>
<summary><h2>Problem</h2></summary>

- [A. Arpa’s hard exam and Mehrdad’s naive cheat](https://codeforces.com/contest/742/problem/A)


</details>

</details>
<details>
    <summary><h1>Euler's Totient Function</h1></summary>
    <img width="893" height="391" alt="image" src="https://github.com/user-attachments/assets/76254e15-ea60-45a4-aac5-50b20b027ab5" />

```cpp
long long eulerTotient(long long n) {
    long long res = n;
    for(long long i = 2; i*i <= n; i++) {
        if(n % i == 0) {
            while(n % i == 0) n /= i;
            res -= res / i;
        }
    }
    if(n > 1) res -= res / n;
    return res;
}
```
<img width="847" height="149" alt="image" src="https://github.com/user-attachments/assets/39cc5ebe-8697-4322-82a6-934a4bf00c43" />

Time Compexity: 

| Concept               | Complexity                             | Purpose / Use Case                       |
| --------------------- | -------------------------------------- | ---------------------------------------- |
| Binary exponentiation | O(log n)                               | Fast power, modular exponentiation       |
| Matrix exponentiation | O(k³ log n)                            | Linear recurrences, DP optimization      |
| Modular arithmetic    | O(1) for add/sub/mul, O(log n) for pow | Keep numbers within bounds, cryptography |
| Euler totient         | O(√n)                                  | Count coprimes, compute modular inverses |
<details>
    <summary><h2>Problem</h2></summary>

- Problem
</details>
</details>

<details>
    <summary><h1>1.0 Basic Number Theory</h1></summary>

# ⭐ Which numbers have an odd number of divisors?

A number has an odd number of divisors if and only if it is a perfect square.

Check if a number has odd divisors:
```cpp
bool hasOddDivisors(long long x) {
    long long r = sqrtl(x);
    return r*r == x;  // true if x is a perfect square
}
```

# [Number of divisors / sum of divisors](https://cp-algorithms.com/algebra/divisors.html#toc-tgt-1)
## Count The Number of Divisors N 

N = p^e1 .p^e2.p^e3 .p^e4.p^e5 ......p^ek

d(n) =(e1+1).(e2+1).(e3+1).(e4+1).(e5+1).(e6+1)....(ek+1)

```cpp
long long numberOfDivisors(long long num)
{
    long long total = 1;
    for (int i = 2; (long long)i * i <= num; i++)
    {
        if (num % i == 0)
        {
            int e = 0;
            while (num % i == 0)
            {
                e++;
                num /= i;
            }
            total *= e + 1;
        }
    }
    if (num > 1)
    {
        total *= 2;
    }
    return total;
}
```
## Sum of The Number of Divisors N

<img width="846" height="146" alt="image" src="https://github.com/user-attachments/assets/5f588249-e26f-4489-89f3-ee17a4e26d0c" />

```cpp
long long SumOfDivisors(long long num)
{
    long long total = 1;

    for (int i = 2; (long long)i * i <= num; i++)
    {
        if (num % i == 0)
        {
            int e = 0;
            do
            {
                e++;
                num /= i;
            } while (num % i == 0);

            int cntSameDivisors = e + 1;

            long long sum = 0, pow = 1;
            
            while (cntSameDivisors--)
            {
                sum += pow;
                pow *= i;
            }
            total *= sum;
        }
    }
    if (num > 1)
    {
        total *= (1 + num);
    }
    return total;
}
```
# Sieve of Eratosthenes (Sieve)
The Sieve of Eratosthenes is an efficient algorithm to find all prime numbers up to a given number n.
```cpp
vector<bool> prime(N+1, true);

void sieve(int N) {
    prime[0] = prime[1] = false;
    for(int i = 2; i * i <= N; i++) {
        if(prime[i]) {
            for(int j = i * i; j <= N; j += i) {
                prime[j] = false;
            }
        }
    }
}
```
🔥 Time Complexity: O(NloglogN)
🔥 Space Complexity: O(N)
# Divisors Count Sieve (1 to N)
```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1e7 + 9;
int divisorsCnt[N];

void divisorSieve()
{
    for (int i = 1; i < N; i++)
    {
        for (int j = i; j < N; j += i)
        {
            divisorsCnt[j]++;
        }
    }
}

int main()
{
    divisorSieve(); // You MUST call this

    cout << divisorsCnt[100] << endl; // Expected output: 9
    return 0;
}

```
Works smoothly up to N = 10⁷ in C++

Time Complexity: O(N log N)

Space: O(N)

# Smallest Prime Factor (SPF) Sieve
```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1e7 + 9;
int spf[N];

void buildSPF()
{
    for (int i = 1; i < N; i++)
        spf[i] = i;

    for (int i = 2; i*I < N; i++)
    {
        if (spf[i] == i)
        { // i is prime
            for (int j = i*i; j < N; j += i)
            {
                if (spf[j] == j) // update only once
                    spf[j] = i;
            }
        }
    }
}

vector<pair<int, int>> primeFactorization(int n)
{
    vector<pair<int, int>> ans;
    while (n > 1)
    {
        int x = spf[n];
        int e = 0;
        while (n % x == 0)
        {
            e++;
            n /= x;
        }
        ans.push_back({x, e});
    }
    return ans;
}

int main()
{
    buildSPF();
    int n;
    cin >> n;

    auto factorize = primeFactorization(n);
    for (auto [p, e] : factorize)
        cout << p << "^" << e << " ";
    cout << endl;
}
```
Time complexity: O(N log N)
Factorization of each number: O(log N)
Very fast for 1e7 or 1e6 constraints.

# Eler's Totient Function

φ(n) = number of integers from 1 to n that are coprime to n
(i.e., gcd(x, n) = 1)

<img width="1289" height="309" alt="image" src="https://github.com/user-attachments/assets/db8bb9d7-cae6-4bcf-9131-ff68b3ab0ad2" />
<img width="1289" height="711" alt="image" src="https://github.com/user-attachments/assets/8bbf9d1c-68aa-4df3-9eae-7cfa4eb3294d" />
<img width="1292" height="670" alt="image" src="https://github.com/user-attachments/assets/5c0370dc-8d1a-437c-9a8b-2eec0f46bd9a" />

### 🧠 Key Formula

If
n = p₁^a₁ × p₂^a₂ × … × pk^ak
(prime factorization)

Then:

<img width="750" height="89" alt="image" src="https://github.com/user-attachments/assets/38dc2248-64d8-4115-82c5-d5ca03551da9" />

Code: 

```cpp
vector<int> phi(N+1);

void computeTotient() {
    for (int i = 1; i <= N; i++) phi[i] = i;

    for (int i = 2; i <= N; i++) {
        if (phi[i] == i) {   
            // i is prime
            for (int j = i; j <= N; j += i) {
                phi[j] -= phi[j] / i;
            }
        }
    }
}
```

<details>
    
<summary><h2>Problem</h2></summary>

- [Problem - A](#)


</details>

</details>

<details>
    <summary><h1>Description</h1></summary>
 <details>
<summary><h2>Problem</h2></summary>

- [Problem - A](#)


</details>

</details>
