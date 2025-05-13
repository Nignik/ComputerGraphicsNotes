## Formula
$$
\mathbf{R}_x(\phi) = \begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & \cos\phi & -\sin\phi & 0 \\
0 & \sin\phi & \cos\phi & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
$$
\mathbf{R}_y(\phi) = \begin{pmatrix}
\cos\phi & 0 & \sin\phi & 0 \\
0 & 1 & 0 & 0 \\
-\sin\phi & 0 & \cos\phi & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
$$
\mathbf{R}_z(\phi) = \begin{pmatrix}
\cos\phi & -\sin\phi & 0 & 0 \\
\sin\phi & \cos\phi & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

## Trace
Trace of a rotation matrix is independent of axis
$tr(\pmb{R}) = 1 + 2cos\phi$

## Example
To rotate an object around point $\mathbf{p}$, it is first necessary to translate object, so that $\mathbf{p}$ is at the origin. Then to rotate, and finally move back to correct coordinates.
$$
\mathbf{X} = \mathbf{T}(\mathbf{p})\mathbf{R}_{z}(\phi)\mathbf{T}(-\mathbf{p})
$$