# Hamming Distance Between Two Numbers

## 1️⃣ What is Hamming Distance?

Hamming distance between two numbers =
number of positions where their binary representations differ

In programming terms:

HammingDistance
```css
HammingDistance(x,y)=popcount(x⊕y)
```
Where:

⊕ = XOR

popcount = number of 1 bits

2️⃣ Why XOR?

Let’s see XOR truth table:

| Bit x | Bit y | x ⊕ y |
| ----- | ----- | ----- |
| 0     | 0     | 0     |
| 1     | 1     | 0     |
| 0     | 1     | 1     |
| 1     | 0     | 1     |


👉 XOR gives 1 only when bits are different

So XOR marks exactly the differing bit positions

3️⃣ Example (Basic)
```css
x = 5  = 101
y = 3  = 011
----------------
x ⊕ y = 110
```

110 has 2 ones

✅ Hamming distance = 2

4️⃣ popcount – counting set bits

In C++:

__builtin_popcount(x);        // int

__builtin_popcountll(x);      // long long


Example:
```cpp
int x = 6; // 110
cout << __builtin_popcount(x); // output: 2
```
## 5️⃣ Hamming Distance Between Two Numbers (Code)
```cpp
int hamming(int a, int b) {
    return __builtin_popcount(a ^ b);
}
```
6️⃣ Problem Meaning: Minimum Hamming Distance Among All Pairs

You are given an array:

a1, a2, ..., an


You must choose two different elements (i ≠ j) such that:

popcount(a[i] ^ a[j]) is minimum

7️⃣ Small Example

Array: [1, 2, 3]

Binary:
```css
1 = 001
2 = 010
3 = 011
```

Pairwise distances:

Pair	XOR	popcount
```css
(1,2)	011	2
(1,3)	010	1
(2,3)	001	1
```
✅ Minimum Hamming distance = 1

## 8️⃣ Important Observations

✔ If two numbers are equal:

x ⊕ x = 0 → popcount = 0


So answer = 0

✔ Minimum possible answer is 0

✔ Maximum possible answer is number of bits (≈30)

9️⃣ Why This Solves Your AND–OR–XOR Problem?

You already proved:
```css
(AND of subsequence) ⊕ (OR of subsequence)
= number of mixed bits
```
For two elements only:

Bit pattern	Result
```css
0 & 0	0
1 & 1	0
0 & 1	1
```
Exactly same as XOR

So:
```css
(AND)⊕(OR)=a[i]⊕a[j]
```
Thus:

Minimize tension → minimize Hamming distance

🔟 Brute Force (For Understanding)
```cpp
int ans = 1e9;
for(int i = 0; i < n; i++) {
    for(int j = i + 1; j < n; j++) {
        ans = min(ans, __builtin_popcount(a[i] ^ a[j]));
    }
}
```

⚠ Too slow for large n, but perfect for learning.

### 1️⃣1️⃣ Efficient Thinking (Contest Insight)

Numbers have only ~30 bits

Most close numbers differ in 1 or 2 bits

Try to find pairs differing by:

0 bits (duplicates)

1 bit

2 bits

That’s why optimized solutions stop early.

1️⃣2️⃣ Real-Life Intuition

Think of each number as a 30-length light switch panel
Hamming distance = how many switches differ

You’re finding the two most similar panels

1️⃣3️⃣ Summary (One Screen)

✅ Hamming distance = popcount(x ^ y)

✅ XOR highlights differences

✅ Minimum tension = minimum XOR bit count

✅ Best subsequence size = 2

If you want next:

🔹 Bitmask tricks

🔹 Trie-based optimization

🔹 CF problems practice list

🔹 Why subsequence > 2 never helps
