# [Creating Triangles](https://lightoj.com/problem/creating-triangles)
stars[k]=2^popcount(k−1)
```rust
k  | n  | value (stars[k]) | k-1 | binary(k-1) | popcount(k-1)
----------------------------------------------------------------
1  | 50 | 1                | 0   | 0           | 0
2  | 50 | 2                | 1   | 1           | 1
3  | 50 | 2                | 2   | 10          | 1
4  | 50 | 4                | 3   | 11          | 2
5  | 50 | 2                | 4   | 100         | 1
6  | 50 | 4                | 5   | 101         | 2
7  | 50 | 4                | 6   | 110         | 2
8  | 50 | 8                | 7   | 111         | 3
9  | 50 | 2                | 8   | 1000        | 1
10 | 50 | 4                | 9   | 1001        | 2
11 | 50 | 4                |10   | 1010        | 2
12 | 50 | 8                |11   | 1011        | 3
13 | 50 | 4                |12   | 1100        | 2
14 | 50 | 8                |13   | 1101        | 3
15 | 50 | 8                |14   | 1110        | 3
16 | 50 | 16               |15   | 1111        | 4
17 | 50 | 2                |16   |10000        | 1
18 | 50 | 4                |17   |10001        | 2
19 | 50 | 4                |18   |10010        | 2
20 | 50 | 8                |19   |10011        | 3
21 | 50 | 4                |20   |10100        | 2
22 | 50 | 8                |21   |10101        | 3
23 | 50 | 8                |22   |10110        | 3
24 | 50 | 16               |23   |10111        | 4
25 | 50 | 4                |24   |11000        | 2
26 | 50 | 8                |25   |11001        | 3
27 | 50 | 8                |26   |11010        | 3
28 | 50 | 16               |27   |11011        | 4
29 | 50 | 8                |28   |11100        | 3
30 | 50 | 16               |29   |11101        | 4
31 | 50 | 16               |30   |11110        | 4
32 | 50 | 32               |31   |11111        | 5
33 | 50 | 2                |32   |100000       | 1
34 | 50 | 4                |33   |100001       | 2
35 | 50 | 4                |34   |100010       | 2
36 | 50 | 8                |35   |100011       | 3
37 | 50 | 4                |36   |100100       | 2
38 | 50 | 8                |37   |100101       | 3
39 | 50 | 8                |38   |100110       | 3
40 | 50 | 16               |39   |100111       | 4
41 | 50 | 4                |40   |101000       | 2
42 | 50 | 8                |41   |101001       | 3
43 | 50 | 8                |42   |101010       | 3
44 | 50 | 16               |43   |101011       | 4
45 | 50 | 8                |44   |101100       | 3
46 | 50 | 16               |45   |101101       | 4
47 | 50 | 16               |46   |101110       | 4
48 | 50 | 32               |47   |101111       | 5
49 | 50 | 4                |48   |110000       | 2
50 | 50 | 8                |49   |110001       | 3
51 | 50 | 8                |50   |110010       | 3
52 | 50 | 16               |51   |110011       | 4
53 | 50 | 8                |52   |110100       | 3
54 | 50 | 16               |53   |110101       | 4
55 | 50 | 16               |54   |110110       | 4
56 | 50 | 32               |55   |110111       | 5
57 | 50 | 8                |56   |111000       | 3
58 | 50 | 16               |57   |111001       | 4
59 | 50 | 16               |58   |111010       | 4
60 | 50 | 32               |59   |111011       | 5
61 | 50 | 16               |60   |111100       | 4
62 | 50 | 32               |61   |111101       | 5
63 | 50 | 32               |62   |111110       | 5
64 | 50 | 64               |63   |111111       | 6


```
value = 1ULL << __builtin_popcountll(k-1)
```cpp
ull stars(ull k)
{
    if (k == 0)
        return 0;
    return 1ULL << __builtin_popcountll(k - 1ULL);
}
```
```cpp
void solve()
{
    ull k;
    unsigned int n;
    cin >> k >> n;
    cout << "Case " << ++cs << ": ";

    ull limit = 1ULL << (n + 2);
    if (k > limit)
    {
        cout << -1 <<endl;
        return;
    }

    cout << stars(k) <<endl;
}
```
## __builtin_popcountll()
 __builtin_popcountll() is a built-in GCC/Clang function that counts how many bits are 1 in a given unsigned long long.

✔ Example
```cpp
unsigned long long x = 13; // binary: 1101
cout << __builtin_popcountll(x);
```

Output: 
```css
3
```
Because:
```css
13 = 1101
       ↑ ↑  ↑
      1 1 0 1  => 3 bits are 1
```

✔ Variants

| function             | type               |
| -------------------- | ------------------ |
| __builtin_popcount   | unsigned int       |
| __builtin_popcountl  | unsigned long      |
| __builtin_popcountll | unsigned long long |

✔ Return type

Returns an int
```cpp
int bits = __builtin_popcountll(x);
```
## __builtin_ctzll(x) — Count Trailing Zeros (for long long)

Counts the number of consecutive 0 bits from the least significant bit (right side) up to the first 1.

Syntax:
```cpp
int __builtin_ctzll(unsigned long long x);
```

Important:

x must be non-zero; otherwise the result is undefined.

Example:
```cpp
unsigned long long x = 40; // binary: 101000
cout << __builtin_ctzll(x) << endl;
```

Step by step:
```css
binary(x) = 101000
LSB → first 1 is at bit 3 (0-indexed from right)
Trailing zeros = 3
```

Output:
```css
3
```

Use cases:

Find the lowest set bit position: 1ULL << __builtin_ctzll(x)

Fast division by powers of two

Bitmask DP, subset generation, optimizing loops

## __builtin_clzll(x) — Count Leading Zeros (for long long)

Definition:
Counts the number of consecutive 0 bits from the most significant bit (left side) up to the first 1.

Syntax:
```cpp
int __builtin_clzll(unsigned long long x);
```

Important:

For unsigned long long, it assumes 64-bit width

x must be non-zero; otherwise undefined behavior

Example:
```cpp
unsigned long long x = 40; // binary: 101000
cout << __builtin_clzll(x) << endl;
```

Step by step (64-bit representation):
```css
x = 0000...00101000
Leading zeros = 58
```

Output:
```css
58
```

Use cases:

Determine bit-length of a number:
```cpp
int bitLength = 64 - __builtin_clzll(x);
```

Efficient comparison / log2 calculation

Bit compression, normalization in floating point simulations

## __builtin_parityll(x) — XOR Parity (for long long)

Computes the parity of number of 1s in binary representation:

Returns 0 if the count of 1s is even

Returns 1 if the count of 1s is odd

Syntax:
```cpp
int __builtin_parityll(unsigned long long x);
```

Example 1:
```cpp
unsigned long long x = 13; // binary: 1101
cout << __builtin_parityll(x) << endl;
```

Step by step:
```css
binary(x) = 1101
Number of 1s = 3 → odd
Parity = 1
```

Output:
```css
1
```


Example 2:
```cpp
unsigned long long x = 14; // binary: 1110
cout << __builtin_parityll(x) << endl;
```
binary(x) = 1110
Number of 1s = 3 → odd
Parity = 1


Output:
```css
1
```

Example 3:
```cpp
unsigned long long x = 15; // binary: 1111
cout << __builtin_parityll(x) << endl;
```
Number of 1s = 4 → even
Parity = 0


Output:
```css
0
```

a literal number in C++ meaning:
| literal | type               |
| ------- | ------------------ |
| 1       | int                |
| 1L      | long               |
| 1LL     | long long          |
| 1U      | unsigned int       |
| 1UL     | unsigned long      |
| 1ULL    | unsigned long long |
