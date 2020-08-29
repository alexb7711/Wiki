# Cramer's Rule
In linear algebra, Cramer's rule is an explicit formula for the solution of a system of lienar equations with as many equations as unknowns, valid whenever the system has a unique solution. 

## Explicit formulas for small systems
Consider the system of equations below

$$
\begin{bmatrix}
  a_1 & b_1
  a_2 & b_2
\end{bmatrix}
*
\begin{bmatrix}
  x \\
  y
\end{bmatrix}
= 
\begin{bmatrix}
  c_1 \\
  c_2
\end{bmatrix}
$$

solving this by taking inverse and determinants we get the equations

$$
x = \frac
{
  \begin{vmatrix}
    c_1 & b_1 \\
    c_2 & b_2
  \end{vmatrix}
}
{
  \begin{vmatrix}
    a_1 & b_1 \\
    a_2 & b_2
  \end{vmatrix}
}
= \frac{c_1 b_2 - b_1 c_2}{a_1 b_2 - b_1 a_2}
$$

and similarly for y

$$
y = \frac
{
  \begin{vmatrix}
    a_1 & c_1 \\
    a_2 & c_2
  \end{vmatrix}
}
{
  \begin{vmatrix}
    a_1 & b_1 \\
    a_2 & b_2
  \end{vmatrix}
}
= \frac{a_1 c_2 - c_1 a_2}{a_1 b_2 - b_1 a_2}
$$

This rule can extend into 3x3 matricies just the same. For more on that click [here](https://en.wikipedia.org/wiki/Cramer%27s_rule)

---
