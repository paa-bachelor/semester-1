# Scipy-guide

**[LEAST SQUARES]**
1,2,3,4 = _scipy.linalg.lstsq(A,b)_ returns 4 objects: 
1. the least squares solution to Ax = b, i.e. the returned array will represent a vector such that the euclidean norm squared of said vector is minimalized (|Ax-b|)

2. residues: Square of the 2-norm for each column in b - a x, if M > N and ndim(A) == n (returns a scalar if b is 1-D). Otherwise a (0,)-shaped array is returned.

3. The effective rank of A

4. An array with singular values of A
