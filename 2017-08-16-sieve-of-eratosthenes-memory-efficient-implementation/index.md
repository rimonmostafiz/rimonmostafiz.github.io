# Sieve of Eratosthenes (Memory Efficient Implementation)

Say we want to find all prime numbers up to an integer **N** where **N** is **10<sup>8</sup>**. If we write a regular implementation of [Sieve Of Eratosthenes](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) using a bool array for each integer in the range `[1:N]` then we could end up using **N** bytes of memory, which would roughly be **95 MB** which is a not a very small memory.

Lets see how can we reduce the memory, the main idea here is we can store a Boolean value in a single bit, so we can store **8 Boolean** values in a single byte. Yet another idea is we know there is only one even prime number which is **2** so we don't need to calculate for other even numbers. With this in mind we can reduce the memory requirement half by simply not storing information for even numbers, but obviously we need to handle this only even number **2** on our own.

With these If we store this information in **4-byte** integers, then we require only **N/32** integers.

~~~
#include <iostream>
#include <cstdio>

using namespace std;

#define MAX 100000000  // 10^8
#define LMT 10000      // sqrt of MAX
#define LEN 5800032    // maximum possible different primes

unsigned flag[MAX>>6], primes[LEN];

#define ifc(n) (flag[n>>6]&(1<<((n>>1)&31)))
#define isc(n) (flag[n>>6]|=(1<<((n>>1)&31)))

void sieve() {
    unsigned i, j, k;
    for(i=3; i<LMT; i+=2)
        if(!ifc(i))
            for(j=i*i, k=(i<<1); j<MAX; j+=k)
                isc(j);
    primes[0] = 2;
    for(i=3, k=1; i<MAX; i+=2)
        if(!ifc(i))
            primes[k++] = i;
}

int main() {
    sieve();
    return 0;
}
~~~
### Explanation:
Lets talk about the these macros first
~~~
#define MAX 100000000 // 10^8
#define LMT 10000 // sqrt of MAX
#define LEN 5800032 // maximum possible different primes
~~~

**MAX** is the maximum range **(10<sup>8</sup>)**, we need to calculate our prime numbers up to MAX
**LMT** is the `sqrt` of MAX, a number **X** is prime if it is not divisible by any prime number up to sqrt of **X**. this is the main idea of  [Sieve Of Eratosthenes](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes).
**LEN** is size of Array we store out primes.

The variable declaration 

    unsigned flag[MAX>>6], primes[LEN];

**flag[MAX>>6]** is actually **flag[MAX/64]** and And why we divide **MAX** by **64** ? <br>
Next the **primes** Array for storing all primes up to **MAX**

Now the super macro, which is doing all the things for us
~~~
#define ifc(n) (flag[n>>6]&(1<<((n>>1)&31)))
#define isc(n) (flag[n>>6]|=(1<<((n>>1)&31)))
~~~
`ifc` checks if a specific bit is 1 or 0 <br>
`isc` sets a specific bit 1 to mark it as composite in flag array.

In bit-wise sieve a specific value **N** located in
**[N/32]<sup>th</sup>** index, and on that index **[N%32]<sup>th</sup>** bit from **LSB**(Right to left). But as we are considering the odd numbers only, we can map **N** with **N/2**.

Now if we replace **N** with **N/2**,

The  **[N/32]th** index now becomes **[N/2/32] = [N/64] = [N>>6]** <br>

And **[N%32]th** bit position becomes **((N/2)%32) = (N>>1)&31**

We know, modding with a power of **2** is same as **AND** ing **(&)** with **(same power of 2)-1**.

But why we are using bit shifting/Operations? :confused: <br>  Because bit is fun and faster. :wink:


This implementation reserves about **[10<sup>8</sup>/64] = [MAX>>64]** integers for the flag array, which is about **6MB** of memory. Since there are **5.8 Million** primes under **10<sup>8</sup>**, this would require an extra **4 x 5.8 x 10<sup>6</sup>** bytes of array(primes array) which is roughly **22 MB** which is obviously far better than **95 MB** :smiley:

