# Generalized Mersenne prime

A prime of the form $p = f(2^m)$, where $f(t)$ is a low-degree polynomial with small interger cofficients.

In pracrice, $m$ is taken to be a multiple of the **word size** of the machine in order to eliminayte the need for shifting bits within words. 

#  Modular reduction

## Example $p = 2^{192} - 2^{64} - 1$

In this case, $f(t) = t^3 - t - 1$, and one has

$$\sum\limits_{i=0}^{5} {c_it^i} \equiv b_2t^2 + b_1t + b_0 \pmod {f(t)},$$

where

$$
\begin{aligned}
& b_0 = a_0 + a_3 + a_5         \\
& b_1 = a_1 + a_3 + a_4 + a_5   \\
& b_2 = a_2 + a_4 + a_5         
\end{aligned}
$$

This yields the following reduction alforithm for $p = f(2^{64})$. A positive integer modulo $p^2$ is represented as the concatenation of 64-bits words

$$(c_5 \ \|\  c_4 \ \|\  c_3 \ \|\  c_2 \ \|\  c_1 \ \|\  c_0),$$
where represents

$$c = \sum\limits_{i = 0}^{5} c_i \cdot 2^{64i}.$$

Then

$$c \equiv s_0 + s_1 + s_2 + s_3 \pmod p.$$

where the $s_i$ is the interger respresented by the following concatentations of the six words:

$$
\begin{aligned}
& s_0 = (c_2 \ \|\  c_1 \ \|\  c_0) \\
& s_1 = (0 \ \|\  c_3 \ \|\  c_3)   \\
& s_2 = (c_4 \ \|\  c_4 \ \|\  0)   \\
& s_3 = (c_5 \ \|\  c_5 \ \|\  c_5)
\end{aligned}
$$


## SM2: $p = 2^{256} - 2^{224} - 2^{96} + 2^{64} - 1$

$p = f(t), t = 2 ^ {32}$. A positive integer $A \in [0, p^2)$.

$$A = \sum\limits_{i = 0}^{15} A_i \cdot t^i.$$

We can obtain the following congruence:

$$
\left\{\begin{array}{l}
t^{8} \equiv t^{7} + t^{3} - t^{2} + 1 \pmod p \\
t^{9} \equiv t^{7} + t^{4} - t^{2} + t + 1 \pmod p \\
t^{10} \equiv t^{7} + t^{5} + t + 1 \pmod p \\
t^{11} \equiv t^{7} + t^{6} + t^{3} + t + 1 \pmod p \\
t^{12} \equiv 2 \cdot t^{7} + t^{4} + t^{3} + t + 1 \pmod p \\
t^{13} \equiv 2 \cdot t^{7} + t^{5} + t^{4}+2 \cdot t^{3} - t^{2} + t + 2 \pmod p \\
t^{14} \equiv 2 \cdot t^{7} + t^{6} + t^{5}+2 \cdot t^{4} + t^{3} - t^{2} + 2 \cdot t + 2 \pmod p \\
t^{15} \equiv 3 \cdot t^{7} + t^{6} + 2 \cdot t^{5} + t^{4} + t^{3} + 2 \cdot t + 2 \pmod p
\end{array}\right.
$$

The matrix form of these congruence is

$$
\left(\begin{array}{c}
t^{8}     \\
t^{9}     \\
t^{10}    \\
t^{11}    \\
t^{12}    \\
t^{13}    \\
t^{14}    \\
t^{15}    \\
\end{array}\right) \equiv\left(\begin{array}{cccccccc}
1 & 0 & -1 & 1 & 0 & 0 & 0 & 1   \\
1 & 1 & -1 & 0 & 1 & 0 & 0 & 1   \\
1 & 1 & 0 & 0 & 0 & 1 & 0 & 1    \\
1 & 1 & 0 & 1 & 0 & 0 & 1 & 1    \\
1 & 1 & 0 & 1 & 1 & 0 & 0 & 2    \\
2 & 1 & -1 & 2 & 1 & 1 & 0 & 2   \\
2 & 2 & -1 & 1 & 2 & 1 & 1 & 2   \\
2 & 2 & 0 & 1 & 1 & 2 & 1 & 3    \\
\end{array}\right)\left(\begin{array}{c}
1       \\
t       \\
t^{2}   \\
t^{3}   \\
t^{4}   \\
t^{5}   \\
t^{6}   \\
t^{7}   \\
\end{array}\right)\pmod p
$$

Therefore, we can obtain

$$\sum\limits_{i = 0}^{15} A_i \cdot t^i \equiv \sum\limits_{i = 0}^{7} B_i \cdot t^i \pmod p.$$

where $B_i$ is given by

$$
(B_0, B_1, \cdots, B_7) = (A_0, A_1, \cdots, A_7) + (A_8, A_9, \cdots, A_{15})
\left(\begin{array}{cccccccc}
1 & 0 & -1 & 1 & 0 & 0 & 0 & 1   \\
1 & 1 & -1 & 0 & 1 & 0 & 0 & 1   \\
1 & 1 & 0 & 0 & 0 & 1 & 0 & 1    \\
1 & 1 & 0 & 1 & 0 & 0 & 1 & 1    \\
1 & 1 & 0 & 1 & 1 & 0 & 0 & 2    \\
2 & 1 & -1 & 2 & 1 & 1 & 0 & 2   \\
2 & 2 & -1 & 1 & 2 & 1 & 1 & 2   \\
2 & 2 & 0 & 1 & 1 & 2 & 1 & 3    \\
\end{array}\right)\
$$

That means

$$
\begin{aligned}
& B_0 = A_0 + A_8 + A_9 + A_{10} + A_{11} + A_{12} + 2A_{13} + 2A_{14} + 2A_{15}, \\
& B_1 = A_1 + A_9 + A_{10} + A_{11} + A_{12} + A_{13} + 2A_{14} + 2A_{15}, \\
& B_2 = A_2 - (A_8 + A_9 + A_{13} + A_{14}), \\
& B_3 = A_3 + A_8 + A_{11} + A_{12} + 2A_{13} + A_{14} + A_{15}, \\
& B_4 = A_4 + A_9 + A_{12} + A_{13} + 2A_{14} + A_{15}, \\
& B_5 = A_5 + A_{10} + A_{13} + A_{14} + 2A_{15}, \\
& B_6 = A_6 + A_{11} + A_{14} + A_{15}, \\
& B_7 = A_7 + A_8 + A_9 + A_{10} + A_{11} + 2A_{12} + 2A_{13} + 2A_{14} + 3A_{15}. \\
\end{aligned}
$$

Thus

$$
\begin{aligned}
\sum\limits_{i = 0}^{7} B_i \cdot t^i = &T + S_1 + S_2 + S_3 + S_4 + S_5 + S_6 + S_7 + S_8 + S_9 + S_{10} + S_{11} + 2S_{12}\\
& - D_1 - D_2 - D_3 - D_4
\end{aligned}
$$

where

$$
\begin{aligned}
& T = (A_7 \ \|\  A_6 \ \|\  A_5 \ \|\  A_4 \ \|\  A_3 \ \|\  A_2 \ \|\  A_1 \ \|\  A_0) \\
& S_1 = (A_8 \ \|\  A_{11} \ \|\  A_{10} \ \|\  A_9 \ \|\  A_8 \ \|\  0 \ \|\  A_9 \ \|\  A_8) \\
& S_2 = (A_9 \ \|\  A_{14} \ \|\  A_{13} \ \|\  A_{12} \ \|\  A_{11} \ \|\  0 \ \|\  A_{10} \ \|\  A_9) \\
& S_3 = (A_{10} \ \|\  A_{15} \ \|\  A_{14} \ \|\  A_{13} \ \|\  A_{12} \ \|\  0 \ \|\  A_{11} \ \|\  A_{10}) \\
& S_4 = (A_{11} \ \|\  0 \ \|\  A_{15} \ \|\  A_{14} \ \|\  A_{13} \ \|\  0 \ \|\  A_{12} \ \|\  A_{11}) \\
& S_5 = (A_{12} \ \|\  0 \ \|\  A_{15} \ \|\  A_{14} \ \|\  A_{13} \ \|\  0 \ \|\  A_{13} \ \|\  A_{12}) \\
& S_6 = (A_{12} \ \|\  0 \ \|\  0 \ \|\  A_{15} \ \|\  A_{14} \ \|\  0 \ \|\  A_{14} \ \|\  A_{13}) \\
& S_7 = (A_{13} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{15} \ \|\  0 \ \|\  A_{14} \ \|\  A_{13}) \\
& S_8 = (A_{13} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{15} \ \|\  A_{14}) \\
& S_9 = (A_{14} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{15} \ \|\  A_{14}) \\
& S_{10} = (A_{14} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{15}) \\
& S_{11} = (A_{15} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{15}) \\
& S_{12} = (A_{15} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0) \\
& D_1 = (0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_8 \ \|\  0 \ \|\  0) \\
& D_2 = (0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_9 \ \|\  0 \ \|\  0) \\
& D_3 = (0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{13} \ \|\  0 \ \|\  0) \\
& D_4 = (0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{14} \ \|\  0 \ \|\  0) 
\end{aligned}
$$

Since doubling can be achieved quickly by shifting, the optimization is

$$
\begin{aligned}
\sum\limits_{i = 0}^{7} B_i \cdot t^i = &T + S_1 + S_2 + S_3 + S_4 + S_5 + 2S_6 + 2S_7 + 2S_8 + 2S_9 \\
& - D_1 - D_2 - D_3 - D_4
\end{aligned}
$$

$$
\begin{aligned}
& T = (A_7 \ \|\  A_6 \ \|\  A_5 \ \|\  A_4 \ \|\  A_3 \ \|\  A_2 \ \|\  A_1 \ \|\  A_0) \\
& S_1 = (A_8 \ \|\  A_{11} \ \|\  A_{10} \ \|\  A_9 \ \|\  A_8 \ \|\  0 \ \|\  A_9 \ \|\  A_8) \\
& S_2 = (A_9 \ \|\  A_{14} \ \|\  A_{13} \ \|\  A_{12} \ \|\  A_{11} \ \|\  0 \ \|\  A_{10} \ \|\  A_9) \\
& S_3 = (A_{10} \ \|\  A_{15} \ \|\  A_{14} \ \|\  A_{13} \ \|\  A_{12} \ \|\  0 \ \|\  A_{11} \ \|\  A_{10}) \\
& S_4 = (A_{11} \ \|\  0 \ \|\  0 \ \|\  A_{15} \ \|\  A_{14} \ \|\  0 \ \|\  A_{12} \ \|\  A_{11}) \\
& S_5 = (A_{15} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{13} \ \|\  A_{12}) \\
& S_6 = (A_{12} \ \|\  0 \ \|\  A_{15} \ \|\  A_{14} \ \|\  A_{13} \ \|\  0 \ \|\  A_{14} \ \|\  A_{13}) \\
& S_7 = (A_{13} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{15} \ \|\  A_{14}) \\
& S_8 = (A_{14} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{15} \ \|\  0 \ \|\  0 \ \|\  A_{15}) \\
& S_9 = (A_{15} \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0) \\
& D_1 = (0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_8 \ \|\  0 \ \|\  0) \\
& D_2 = (0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_9 \ \|\  0 \ \|\  0) \\
& D_3 = (0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{13} \ \|\  0 \ \|\  0) \\
& D_4 = (0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  0 \ \|\  A_{14} \ \|\  0 \ \|\  0) 
\end{aligned}
$$

# Reference

1. Encyclopedia of cryptography and security[M]. Springer Science & Business Media, 2014.
2. Solinas J A. Generalized mersenne numbers[M]. Faculty of Mathematics, University of Waterloo, 1999.
3. 国家密码管理局. SM2 椭圆曲线公钥密码算法第5 部分: 参数定义: GMT 0003.5-2012[S].
北京:中国标准出版社, 2012:8.
