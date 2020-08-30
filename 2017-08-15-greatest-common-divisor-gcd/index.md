# Greatest Common Divisor (GCD)


Greatest Common Divisor (GCD) of two number a and b is the largest number that divides both a and b evenly.

if `g = gcd(a, b)`, then g divides both a and b when at least one of them is non zero.

when `gcd(a, b) == 1` then we said a and b is co-prime or relatively prime numbers.

~~~~
int gcd (int a, int b) {
    int g;
    for (int i = 1; i <= min(a, b); i++) {
        if (a%i == 0 && b%i == 0) {
          g = i;
        }
  }
  return g;
}
~~~~

Now there is a much more efficient algorithm for finding GCD which is called Subtraction-based Euclidean algorithm.

  * For GCD of **a** and **b** first of all we need to think a grid of size **a × b**.
  * Now we want to cover the grid with square tile. we assume **a** is greater then **b**.
  * We first attempt to tile the **a × b** rectangle using **b × b** square tiles,
  * This leaves an **r0 × b** residual rectangle un-tiled, where **r0<b**.
  * Then we attempt to tile the un-tiled part of the **a x b** rectangle by **r0 x r0** square tiles.
  * Which leaves an **r1 x r0 **residual rectangle un-tiled (now this time **r1<r0**) and so on.

The sequence ends when there is no residual rectangle, i.e., when the square tiles cover the previous residual rectangle exactly. The length of the sides of the smallest square tile is the GCD of the dimensions of the original rectangle.



### _**Example:**_

Now we will try to find the greatest common divisor of `a = 1071` and `b = 462`. ( we are assuming that the **a>b** )

![Euclidean algorithm](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1c/Euclidean_algorithm_1071_462.gif/256px-Euclidean_algorithm_1071_462.gif)

__*Euclidean Algorithm for GCD*__<br>
**Animation : wikimedia**

**STEP 0:**<br>
First the multiples of **b(462)** are subtracted from **a(1071)** until the remainder is less than **b(462)**. Two such multiples can be subtracted **(q<sub>0</sub> = 2)**, leaving a remainder of 147:
`1071 = 2 × 462 + 147`.

**STEP 1:**<br>
Then multiples of 147 are subtracted from 462 until the remainder is less than 147. Three multiples can be subtracted **(q<sub>1</sub> = 3)**, leaving a remainder of 21:
`462 = 3 × 147 + 21`.


**STEP 2:**<br>
Then multiples of 21 are subtracted from 147 until the remainder is less than 21. Seven multiples can be subtracted **(q<sub>2</sub> = 7)**, leaving no remainder:
`147 = 7 × 21 + 0`.

Since the last remainder is zero, the algorithm ends with 21 as the greatest common divisor of 1071 and 462.


| Step k| Equation                                | Quotient and remainder                    |
| ------|:---------------------------------------:|:-----------------------------------------:|
| 0     | 1071 = q<sub>0</sub> 462 + r<sub>0</sub>| q<sub>0</sub> = 2 and r<sub>0</sub> = 147 |
| 1     | 426 = q<sub>1</sub> 147 + r<sub>1</sub> | q<sub>1</sub> = 3 and r<sub>1</sub> = 21  |   
| 2     | 147 = q<sub>2</sub> 21 + r<sub>2</sub>  | q<sub>2</sub> = 7 and r<sub>2</sub> = 0   |

~~~~
/*GCD using Euclidean Algorithm*/
int gcd( int a, int b ) {
    while ( true ) {
        int r = a % b;
        if ( r == 0 ) {
            return b;
        }
        else {
            a = b; // putting larger one in a
            b = r; // putting smaller one in b
        }
    }
}
~~~~

There is an recursive representation of this algorithms

~~~~
int gcd(int a, int b) {
  if( b == 0 )
    return a;
  else
    return gcd( b, a % b );
}
~~~~
this can be write like

~~~~
int gcd( int a, int b ) {
  return b==0 ? a : gcd( b, a % b );
}
~~~~

There is some problem in above code for GCD, that will only works for Int, if you want to find GCD for Long Long then you need to implement above for Long Long Int. Or you can write a template for GCD which will work for both Int and Long Long Int

~~~~
#include <cstdio>
template < class T > T gcd(T a, T b) { return (b != 0 ? gcd<T>(b, a%b) : a); }
int main() {
    // your code here
    return 0;
}
~~~~
In GNU compiler there is a builtin function for calculating GCD
~~~~
int g = __gcd(a, b);
// don't forget to include algorithm header
~~~~

