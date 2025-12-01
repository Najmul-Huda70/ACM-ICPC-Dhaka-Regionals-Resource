# [Aspect Ratio](https://lightoj.com/problem/aspect-ratio)
🧠 Problem Explanation

You had two identical rectangular monitors, each with:
```css
Width = W

Height = H

Diagonal = d

By Pythagorean theorem:

d² = W² + H²


You placed them side-by-side, so the new combined screen has:

Width = 2W

Height = H

Diagonal = k⋅d

Again using Pythagoras:

(kd)² = (2W)² + H²

🔍 Derivation of formula

Original:

W² + H² = d²        ...(1)


Combined:

4W² + H² = k² d²    ...(2)


Multiply equation (1) by 4:

4W² + 4H² = 4d²     ...(3)


Subtract (2) from (3):

(4W² + 4H²) - (4W² + H²) = 4d² - k² d²

3H² = d²(4 - k²)

H² = d²(4 - k²)/3


Using (1):

W² = d² - H²
    = d² - d²(4 - k²)/3
    = d²(k² - 1)/3


Now aspect ratio:

r = H/W


So:

r = sqrt( (H²) / (W²) )
  = sqrt( (4 - k²) / (k² - 1) )


But your code computes the inverse:

x = W/H = sqrt( (k² - 1)/(4 - k²) )


And prints:

x


So your printed value is:

aspect = Width / Height

🧪 Example with sample input:
k = 1.25


Compute:

x = sqrt( (k² - 1)/(4 - k²) )
  = sqrt( (1.5625 - 1)/(4 - 1.5625) )
  = sqrt( 0.5625 / 2.4375 )
  = sqrt(0.230769)
  = 0.480384


Rounded to 4 decimals:

0.4804


This matches:

Case 1: 0.4804
```
# Solution
```cpp
void solve()
{
    double k;
    cin >> k;
    double r = sqrtl((k * k - 1) / (4 - k * k));
    cout << "Case " << ++cs << ": " << fixed << setprecision(4) << r << endl;
}
```
