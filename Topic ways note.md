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
<details>
    <summary><h2>Problem</h2></summary>

- Problem
</details>
</details>


| Concept               | Complexity                             | Purpose / Use Case                       |
| --------------------- | -------------------------------------- | ---------------------------------------- |
| Binary exponentiation | O(log n)                               | Fast power, modular exponentiation       |
| Matrix exponentiation | O(k³ log n)                            | Linear recurrences, DP optimization      |
| Modular arithmetic    | O(1) for add/sub/mul, O(log n) for pow | Keep numbers within bounds, cryptography |
| Euler totient         | O(√n)                                  | Count coprimes, compute modular inverses |

<details>
    <summary><h1>Description</h1></summary>
    <details>
    
<summary><h2>Problem</h2></summary>

- [Problem - A](#)


</details>

</details>
