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
3. 


## Methods tried:

1. A simple iterative scoring based method to get an idea of how many iterations to run. Errors drawn from a discrete gaussian are added to $b$ to give $b'$ and the equation $Ax = b'$ is solved using least-squares. Each time specific entries of $x$ are 0 or 1, their respective scores are incremented at after some iterations, a "solution" consisting of entries with the highest score between 0 and 1 is tested against the actual secret $S$
2. 