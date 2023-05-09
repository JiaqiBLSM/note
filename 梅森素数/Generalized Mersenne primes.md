# Generalized Mersenne prime

A prime of the form $p = f(2^m)$, where $f(t)$ is a low-degree polynomial with small interger cofficients.

In pracrice, $m$ is taken to be a multiple of the **word size** of the machine in order to eliminayte the need for shifting bits within words. 

#  Modular reduction

## Example $p = 2^{192} - 2^{64} - 1$

In this case, $f(t) = t^3 - t - 1$, and one has
$$\sum\limits_{i=0}^{5} {c_it^i} \equiv b_2t^2 + b_1t + b_0 \pmod {f(t)},$$
where
$$b_0 = a_0 + a_3 + a_5$$
$$b_1 = a_1 + a_3 + a_4 + a_5$$
$$b_2 = a_2 + a_4 + a_5$$

This yields the following reduction alforithm for $p = f(2^{64})$. A positive integer modulo $p^2$ is represented as the concatenation of 64-bits words
$$(c_5, c_4, c_3, c_2, c_1, c_0),$$
where represents
$$c = \sum\limits_{i = 0}^{5} c_i \cdot 2^{64i}.$$

Then
$$c \equiv s_0 + s_1 + s_2 + s_3 \pmod p.$$
where the $s_i$ is the interger respresented by the following concatentations of the six words:
$$s_0 = (c_2\quad c_1\quad c_0)$$
$$s_1 = (0\quad c_3\quad c_3)$$
$$s_2 = (c_4\quad c_4\quad 0)$$
$$s_3 = (c_5\quad c_5\quad c_5)$$



