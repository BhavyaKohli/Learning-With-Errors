# Learning With Errors (LWE)

## Problem description:

Guessing/Estimating $S$ given $A$, $b$ and the error distribution of $e$ from

$$
A \times S + e = b
$$

where $A\in \mathbb{Z}_q^{m\times n}$ for prime $q$ and error $e\in \mathbb{Z}_q^{n\times1}$ is drawn from a discrete gaussian distribution $\chi$ with parameter $\sigma\approx 0.05\;q$.

## Material reviewed:

1. https://cims.nyu.edu/~regev/papers/lwesurvey.pdf<br>
	A Survey which serves a great introduction to the problem, naive and a few more complicated methods of solving it. It also discusses the hardness of the problem and its applicaions in cryptography.
2. https://people.csail.mit.edu/vinodv/CS294/lecture2.pdf<br>
	An overview of several different algorithms which can be used to attack an LWE instance.
3. Regev, Oded. "On lattices, learning with errors, random linear codes, and cryptography." Journal of the ACM (JACM) 56.6 (2009): 1-40.
4. Bi, Lei, et al. "Hybrid dual attack on LWE with arbitrary secrets." Cybersecurity 5.1 (2022): 1-27.
5. Albrecht, Martin R., Rachel Player, and Sam Scott. "On the concrete hardness of learning with errors." Journal of Mathematical Cryptology 9.3 (2015): 169-203.


## Methods tried:

1. A simple iterative scoring based method to get an idea of how many iterations to run. Errors drawn from a discrete gaussian are added to $b$ to give $b'$ and the equation $Ax = b'$ is solved using least-squares. Each time specific entries of $x$ are 0 or 1, their respective scores are incremented at after some iterations, a "solution" consisting of entries with the highest score between 0 and 1 is tested against the actual secret $S$.
2. Finding matrices $x_i$ s.t. $A^T \times x_i = u_i$, where $x_i$ has a "small enough" norm. This can be used as follows, and if $e^T \times x_i$ is small enough, we could estimate $S^T_i$ by seeing if the result of $b^T \times x_i$ is closer to 0 or 1.
$$
\begin{align*}
b &= A \times S + e \\
b^T &= S^T \times A^T + e^T \\
b^T \times x_i &= S^T \times u_i + e^T \times x_i \\
b^T \times x_i &= S^T_i + e^T \times x_i \\
\end{align*}
$$
2. (contd)<br>**Problem**: norms of $e^T \times x_i$ are close to 1 for higher values of sigma, and since $S^T_i$ is a binary value, it is too high..<br>**Idea**: Any way of using pdf of $e$ (gaussian) to find error probability or make guesses based on output?
3. Finding $x_i$ s.t. $A^T \times x_i = u_i+u_{i+1}$, therefore we will get $S^T_i + S^T_{i+1}$ instead of just $S^T_i$. Norms are lesser (per value, if that has any effect), experiments underway... Update: poor performance, ~50% accuracy
5. Encryption scheme using LWE, setup scheme for encrypting text, analyzed effects of params on decryption accuracy
4. TODO BKW, explore arora-ge
