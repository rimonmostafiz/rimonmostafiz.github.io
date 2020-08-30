# Least Common Multiple (LCM)


Least Common Multiple (LCM) of two number a and b is the smallest positive integer that is divisible by both a and b. Since division of integers by zero is undefined, this definition has meaning only if a and b are both different from zero.

~~~
int lcm(int a, int b) {
  for ( int i = 1; ; i   ) {
    if ( i % a == 0 && i % b == 0 ) {
      return i;
    }
  }
}
~~~

There is an another technique for LCM finding called Reduction by the greatest common divisor

~~~
int lcm(int a, int b) {
  return a * b / gcd(a, b); // so we need to write gcd() function for this one
}
~~~

there is a chance of integer overflow if we write `a * b / gcd(a, b)`
so we write it like
~~~
int lcm(int a, int b) {
  return (a / gcd(a, b)) * b;
}
~~~

the above code works fine for Int, but it is safe to write a template for LCM, I personally prefer that

~~~
#include <cstdio>

template < class T > T gcd(T a, T b) { return (b != 0 ? gcd<T>(b, a%b) : a); } // need to include GCD also for LCM
template < class T > T lcm(T a, T b) { return (a / gcd<T>(a, b) * b); }

int main() {
    // your code here
    return 0;
}
~~~

