## Formula

$$
\mathbf{S}(\mathbf{s}) = \begin{pmatrix}
s_{x} & 0 & 0 & 0 \\
0 & s_{y} & 0 & 0 \\
0 & 0 & s_{z} & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
$$
\mathbf{S}^{-1}(\mathbf{s}) = \mathbf{S}\left( \frac{1}{s_{x}}, \frac{1}{s_{y}}, \frac{1}{s_{z}} \right)
$$
## Reflection matrix
If $\mathbf{s}$ has 1 or 3 components negative, then $\mathbf{s}$ is a _reflection matrix_. That type of matrix, requires special treatment, as it can cause problems with triangle vertices order. To determine whether, the matrix is reflective, one simply needs to compute determinant of the upper $3\times3$  matrix. If it comes out negative, then the matrix is reflective.

## Scaling in other directions
Lets say that we want to scale along 3 orthonormal right oriented vectors $\mathbf{f}^x, \mathbf{f}^y, \mathbf{f}^z$. First construct the matrix $\mathbf{F}$, to change the basis.
$$
\mathbf{F} = \begin{pmatrix}
\mathbf{f}^x & \mathbf{f}^y & \mathbf{f}^z & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
Then we can perform desired scaling operation.
$$
\mathbf{X} = \mathbf{F}\mathbf{S(\mathbf{s})}\mathbf{F}^T
$$