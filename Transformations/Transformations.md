## Common Transformations

| Notation                                              | Name                     | Characteristics                                     |
| ----------------------------------------------------- | ------------------------ | --------------------------------------------------- |
| $\mathbf{R}_x(\rho)$                                  | rotation matrix          | rotates $\rho$ radians around $x$ axis              |
| $\mathbf{S}(s)$                                       | scaling matrix           | scales along all axes                               |
| $\mathbf{H}_{ij}(s)$                                  | shear matrix             | shears component i by factor s with respect to j    |
| $\mathbf{E}(h, p, r)$                                 | Euler transform          | orientation matrix given by Euler angles            |
| $\mathbf{P}_o(s)$                                     | orthographics projection | parallel projects onto some plane or volume         |
| $\mathbf{P}_p(s)$                                     | perspective projection   | projects with perspective onto some plane or volume |
| $\text{slerp}(\hat{\mathbf{q}}, \hat{\mathbf{r}}, t)$ | slerp transform          | creates interpolated quaternion                     |

$$
\mathbf{X} = \mathbf{F}\mathbf{S(\mathbf{s})}\mathbf{F}^T
$$
## Concatenation of transforms
$$
\mathbf{C} = \mathbf{TRS}
$$
## Orienting the camera
Let camera, be located at $\mathbf{c}$, and we want it to look at $\mathbf{l}$, given camera up direction $\mathbf{u}'$. We want to compute the basis $\{\mathbf{r}, \mathbf{u}, \mathbf{v}\}$.
$\mathbf{v}$ - view vector (normalized vector from the target to camera)
$\mathbf{r}$ - vector looking right
$$
\mathbf{v} = \frac{\mathbf{c - l}}{||\mathbf{c - l}||}
$$
$$
\mathbf{r} = -\frac{\mathbf{v \times u'}}{||\mathbf{v \times u}||}
$$
$$
\mathbf{u} = \mathbf{v} \times \mathbf{r}
$$
Now we can compute camera transform matrix.
$$
\mathbf{M} = \begin{pmatrix}
r_{x} & r_{y} & r_{z} & 0 \\
u_{x} & u_{y} & u_{z} & 0 \\
v_{x} & v_{y} & v_{z} & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
1 & 0 & 0 & -t_{x} \\
0 & 1 & 0 & -t_{y} \\
0 & 0 & 1 & -t_{z} \\
0 & 0 & 0 & 1
\end{pmatrix} = \begin{pmatrix}
r_{x} & r_{y} & r_{z} & -\mathbf{t \cdot r} \\
u_{x} & u_{y} & u_{z} & -\mathbf{t \cdot u} \\
v_{x} & v_{y} & v_{z} & -\mathbf{t \cdot v}  \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
## Normal Transform
Multiplying the surface normal vector by the same transform matrix as the object, will sometimes yield incorrect results. For that the normal, needs to be multiplied by the transpose, of matrix's adjoint. This is only the case, if the transform is a stretch or squash (for example).

## Computation of inverses
- If the matrix is a combination of simple transforms, we can get the inverse, by inverting the parameters and multiplication order.
- If the matrix is orthogonal, then $\mathbf{M}^{-1} = \mathbf{M}^T$
- If nothing is known, then adjoint method, Cramer's rule, LU decomposition or Gaussian elimination can be used.
## Vertex Blending
Let $\mathbf{p}$ be the original vertex and $\mathbf{u}(t)$, the transformed vertex.
$$
\mathbf{u}(t) = \sum_{i=0}^{n-1}w_{i}\mathbf{B}_{i}(t)\mathbf{M}_{i}^{-1}\mathbf{p}, \ \text{where} \sum_{i=0}^{n-1}w_{i} = 1
$$
$w_{i}$ are weights of the bones, $\mathbf{M}_{i}$ is the matrix that transforms bone coordinate system to the world coordinate system. The $\mathbf{B}_{i}$ matrix is the bone world transform, that changes over time.

## Morphing
To compute a morphed vertex for time $t \in [t_{0}, t_{1}]$, compute $s = \frac{t-t_{0}}{t_{1}-t_{0}}$, and then blend.
$$
\mathbf{m} = (1-s)\mathbf{p_{0}} + s\mathbf{p_{1}}
$$

