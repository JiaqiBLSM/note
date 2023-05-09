# Definition

A prime of the form $p = 2^m -k$, where $k$ is an inerger for which $0 < \left| k \right| < 2^{\lfloor \frac{m}{2} \rfloor}$. 

* If $k = 1$ and $m$ is a prime, then $p$ is a Mersenne Prime.
* If $k = -1$ and $m$ is a power of two, then $p$ is a Fermat Prime.
* Otherwise, we say $p$ is a pseudo-Mersenne Prime.

# Fast modular reduction of pseudo-Mersenne Prime

For a integer $n$ where $0 < n < p^2$, when $k > 0$, then $n$ can be written
$$n = a \cdot 2^m + b$$
Then
$$n \equiv a \cdot k + b \pmod{p}$$

Repeating this substitution a few times will yield $n$ modulo $p$. This method of modular reduction requires a small number of additions and subtractions rather than the usual integer division step.

# Pseudocode

``` js
//r = n mod p
Function mod(n, p) {
    r = n;
    low = 0;
    high = 0;
    while r >= 2^m {
        low = r & (2^m - 1);
        high = r >> m;
        r = low + high * (2^m - p)
    }
    if r >= p {
        r = r - p;
    }
    else {
        r = n;
    }
}
```