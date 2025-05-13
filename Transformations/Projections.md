## Orthographic Projection
#### Basic version
$$
\mathbf{P}_{0} = \begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
#### Useful version
$n$ - near plane
$f$ - far plane
$$
\mathbf{P}_{0} = \mathbf{S}(\mathbf{s})\mathbf{T}(\mathbf{t}) = \begin{pmatrix}
\frac{2}{r-l} 0 & 0 & -\frac{r+l}{r-l} \\
0 & \frac{2}{t-b} & 0 & -\frac{t+b}{t-b} \\
0 & 0 & \frac{2}{f-n} & -\frac{f+n}{f-n} \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
#### Perspective projection
$$
\mathbf{P}_{p} = \begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & -\frac{1}{d} & 0
\end{pmatrix}
$$
##### Eye physical field of view
$$
\phi = 2\arctan\left( \frac{w}{2d} \right)
$$
$\phi$ - field of view
$w$ - width of object perpendicular to the line of sight
$d$ - distance to the object

##### Frustum to unit cube
$$
\mathbf{P}_p =
\begin{pmatrix}
\frac{2n}{r - l} & 0 & \frac{r + l}{r - l} & 0 \\
0 & \frac{2n}{t - b} & \frac{t + b}{t - b} & 0 \\
0 & 0 & \frac{t - b}{t - b} & -2n \\
0 & 0 & 1 & 0
\end{pmatrix}.
$$
$$
\mathbf{p} = \left( \frac{q_{x}}{q_{w}}, \frac{q_{y}}{q_{w}}, \frac{q_{z}}{q_{w}}, 1 \right)
$$