# Systems of Linear Equations and Matrices
## Rules of Matrix Arithmetic
1) $A \pm  B = B \pm A$
2) $(A \pm B) \pm C = A \pm (B \pm C)$
3) $A(BC) = (AB)C$
4) $A(B\pm C) = (AB \pm AC)$
5) $(B\pm C)A = BA \pm CA$
6) $a(A \pm B) = aA \pm aB$
7) $ab(C) = a(bC)$
8) $a(BC) = (aB)C = B(aC)$

> A product of invertible matrices is always invertible, and the inverse of the product is the product of the inverse in reverse order.

## Elementary Matrices and Method for Finding $A^-1$
Definition
> An $nxn$ matrix is called an *elementary matrix* if it can be obtained from the $nxn$ identity matrix by performing a single elementary row operation.

Theorem
> If the elementary matrix $E$ results from performing a certain row operation on $I_m$ and if A is an $mxn$ matrix, the product $EA$ is the matrix that results when this same row operation is performed on A.

### Example
Consider the matrix

$$
A = \begin{bmatrix}
1 & 0  & 2 & 3 \\
2 & -1 & 3 & 6 \\
1 & 4  & 4 & 0 \\
\end{bmatrix}
$$

and consider the elementary matrix

$$
E = \begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
3 & 0 & 1 \\
\end{bmatrix}
$$

which results in adding 3 times the first row of $I_3$ to the third row. This product $EA$ is then

$$
EA = \begin{bmatrix}
1 & 0  & 2  & 3 \\
2 & -1 & 3  & 6 \\
4 & 4  & 10 & 9 \\
\end{bmatrix}
$$

***Remark***: Theorem 8 is primarily of theoretical interest and will be used for developing some results about matrices of linear equations.

Theorem
> Every elementary matrix is invertible, and the inverse is also an elementary matrix.

Matrices that can be obtained from one another by a finite sequence of elementary row operations are said to be *row equivalent*.

The inverse of a matrix can be found by multiplying it by a sequence of elementary matrices until the identity matrix is created.
$$
A^{-1} = E_1 \cdot E_n I_n
$$

## Further Results on Systems of Equations and Invertibility
If we have a square, invertible matrix and an equation

$$
AX = B
$$

then we can say 

$$ 
X = A^-1 B 
$$



# References
* Elementary Linear Algebra - Howard Anton
