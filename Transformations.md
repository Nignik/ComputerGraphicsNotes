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
## Translation
#### Formula
$$
\mathbf{T}(\mathbf{t}) = \begin{pmatrix}
1 & 0 & 0 & t_x \\
0 & 1 & 0 & t_y \\
0 & 0 & 1 & t_z \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

## Rotation
#### Formula
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

#### Trace
Trace of a rotation matrix is independent of axis
$tr(\pmb{R}) = 1 + 2cos\phi$

#### Example
To rotate an object around point $\mathbf{p}$, it is first necessary to translate object, so that $\mathbf{p}$ is at the origin. Then to rotate, and finally move back to correct coordinates.
$$
\mathbf{X} = \mathbf{T}(\mathbf{p})\mathbf{R}_{z}(\phi)\mathbf{T}(-\mathbf{p})
$$
## Scaling
#### Formula

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
#### Reflection matrix
If $\mathbf{s}$ has 1 or 3 components negative, then $\mathbf{s}$ is a _reflection matrix_. That type of matrix, requires special treatment, as it can cause problems with triangle vertices order. To determine whether, the matrix is reflective, one simply needs to compute determinant of the upper $3\times3$  matrix. If it comes out negative, then the matrix is reflective.

#### Scaling in other directions
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
## Shearing
#### Formula
$$
\mathbf{H}_{xz}(s) = \begin{pmatrix}
1 & 0 & s & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
$$
\mathbf{H}_{xy}(s, t) = \begin{pmatrix}
1 & 0 & s & 0 \\
0 & 1 & t & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
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
## Euler Transform
#### Formula
$$
\mathbf{E}(h, p, r) = \mathbf{R}_{z}(r)\mathbf{R}_{x}(p)\mathbf{R}_{y}(h)
$$
$$
\mathbf{E}^{-1} = \mathbf{E}^T
$$
_head_: y-roll, yaw
_pitch_: x-roll
_roll_: z-roll

#### Extracting Parameters
$$
\begin{array}{lcl}
h & = & \text{atan}2(-e_{20}, e_{22}) \\
p & = & \arcsin(e_{21}) \\
r & = & \text{atan}2(-e_{01}, e_{11})
\end{array}
$$
#### Rotation Around Arbitrary Axis
$$
\bar{\mathbf{s}} = 
\begin{cases}
(0, -r_z, r_y), & \text{if } |r_x| \leq |r_y| \text{ and } |r_x| \leq |r_z|, \\
(-r_z, 0, r_x), & \text{if } |r_y| \leq |r_x| \text{ and } |r_y| \leq |r_z|, \\
(-r_y, r_x, 0), & \text{if } |r_z| \leq |r_x| \text{ and } |r_z| \leq |r_y|,
\end{cases}
$$
$$
\begin{array}
\mathbf{s} = \frac{\bar{\mathbf{s}}}{\|\bar{\mathbf{s}}\|}, \quad \\
\mathbf{t} = \mathbf{r} \times \mathbf{s}.
\end{array}
$$
$$
\mathbf{M} = \begin{pmatrix}
\mathbf{r}^T \\
\mathbf{s}^T \\
\mathbf{t}^T
\end{pmatrix}
$$
$$
\mathbf{X} = \mathbf{M}^T\mathbf{R}_{x}(\alpha)\mathbf{M}
$$
## Quaternions
#### Definitions
$$
\begin{array}{lcl}
\hat{\mathbf{q}} & = & (\mathbf{q}_{v}, q_{w}) = iq_{x} + jq_{y} + kq_{z} + q_{w} = \mathbf{q}_{v} + q_{w} \\
\mathbf{q}_{v} & = & iq_{x} + jq_{y} + kq_{z} = (q_{x}, q_{y}, q_{z}) \\
i^2 & = & j^2 = k^2 = -1, jk = -kj = i, ki = -ik = j, ij = -ji = k
\end{array}
$$
$q_{w}$ - real part
$\mathbf{q}_{v}$ - imaginary part
$i, j, k$ - imaginary units
#### Useful Equations
$$

\hat{\mathbf{q}} \hat{\mathbf{r}} = (\mathbf{q}_v \times \mathbf{r}_v + r_w \mathbf{q}_v + q_w \mathbf{r}_v, \ q_w r_w - \mathbf{q}_v \cdot \mathbf{r}_v)
$$
$$
\hat{\mathbf{q}} + \hat{\mathbf{r}} = (\mathbf{q}_v, q_w) + (\mathbf{r}_v, r_w) = (\mathbf{q}_v + \mathbf{r}_v, q_w + r_w)
$$
$$
\hat{\mathbf{q}}^* = (\mathbf{q}_v, q_w)^* = (-\mathbf{q}_v, q_w)
$$
$$
n(\hat{\mathbf{q}}) = \sqrt{\hat{\mathbf{q}} \hat{\mathbf{q}}^*} = \sqrt{\hat{\mathbf{q}}^* \hat{\mathbf{q}}} = \sqrt{\mathbf{q}_v \cdot \mathbf{q}_v + q_w^2} = \sqrt{q_x^2 + q_y^2 + q_z^2 + q_w^2}
$$
$$
\hat{\mathbf{i}} = (\mathbf{0}, 1)
$$
$$
\hat{\mathbf{q}}^{-1} = \frac{1}{n(\hat{\mathbf{q}}^2)}\hat{\mathbf{q}}^*
$$
$$
(\hat{\mathbf{q}}^*)^* = \hat{\mathbf{q}}
$$
$$
(\hat{\mathbf{q}} + \hat{\mathbf{r}})^* = \hat{\mathbf{q}}^* + \hat{\mathbf{r}}^*
$$
$$
(\hat{\mathbf{q}} \hat{\mathbf{r}})^* = \hat{\mathbf{r}}^* \hat{\mathbf{q}}^*
$$
$$
n(\hat{\mathbf{q}}^*) = n(\hat{\mathbf{q}})
$$
$$
n(\hat{\mathbf{q}} \hat{\mathbf{r}}) = n(\hat{\mathbf{q}}) n(\hat{\mathbf{r}})
$$
$$
\hat{\mathbf{p}}(s \hat{\mathbf{q}} + t \hat{\mathbf{r}}) = s \hat{\mathbf{p}} \hat{\mathbf{q}} + t \hat{\mathbf{p}} \hat{\mathbf{r}}
$$
$$
(s \hat{\mathbf{p}} + t \hat{\mathbf{q}}) \hat{\mathbf{r}} = s \hat{\mathbf{p}} \hat{\mathbf{r}} + t \hat{\mathbf{q}} \hat{\mathbf{r}}
$$
$$
\hat{\mathbf{p}}(\hat{\mathbf{q}} \hat{\mathbf{r}}) = (\hat{\mathbf{p}} \hat{\mathbf{q}}) \hat{\mathbf{r}}
$$
$$
\hat{\mathbf{q}} = (\sin \phi \mathbf{u}_q, \cos \phi) = \sin \phi \mathbf{u}_q + \cos \phi, \ \text{if} \ n(\hat{\mathbf{q}}) = 1
$$
$$
n(\hat{\mathbf{q}}) = n(\sin \phi \mathbf{u}_q, \cos \phi) = \sqrt{\sin^2 \phi (\mathbf{u}_q \cdot \mathbf{u}_q) + \cos^2 \phi} = \sqrt{\sin^2 \phi + \cos^2 \phi} = 1, \ \text{if} \ ||\mathbf{u}_{q}|| = 1
$$
$$
\hat{\mathbf{q}} = \sin \phi \mathbf{u}_q + \cos \phi = e^{\phi \mathbf{u}_q}
$$
$$
\log(\hat{\mathbf{q}}) = \log(e^{\phi \mathbf{u}_q}) = \phi \mathbf{u}_q
$$
$$
\hat{\mathbf{q}}^t = (\sin \phi \mathbf{u}_q + \cos \phi)^t = e^{t \phi \mathbf{u}_q} = \sin(t \phi) \mathbf{u}_q + \cos(t \phi)
$$
#### Quaternion Transformations
##### Rotations
$\hat{\mathbf{q}}\hat{\mathbf{p}}\hat{\mathbf{q}}^{-1}$ rotates $\hat{\mathbf{p}}$ around the axis $\mathbf{u}_{q}$ by angle $2\phi$.
Given two unit quaternions $\hat{\mathbf{q}}, \ \hat{\mathbf{r}}$ the concatenation of first applying $\hat{\mathbf{q}}$ is:
$$
\hat{\mathbf{r}} (\hat{\mathbf{q}} \hat{\mathbf{p}} \hat{\mathbf{q}}^*) \hat{\mathbf{r}}^* = (\hat{\mathbf{r}} \hat{\mathbf{q}}) \hat{\mathbf{p}} (\hat{\mathbf{r}} \hat{\mathbf{q}})^* = \hat{\mathbf{c}} \hat{\mathbf{p}} \hat{\mathbf{c}}^*, \ \text{where} \ \hat{\mathbf{c}} = \hat{\mathbf{r}}\hat{\mathbf{q}}
$$
##### Quaternion rotation as a matrix
For unit quaternions it is:
$$
\mathbf{M}^{\mathbf{q}} =
\begin{pmatrix}
1 - 2(q_y^2 + q_z^2) & 2(q_x q_y - q_w q_z) & 2(q_x q_z + q_w q_y) & 0 \\
2(q_x q_y + q_w q_z) & 1 - 2(q_x^2 + q_z^2) & 2(q_y q_z - q_w q_x) & 0 \\
2(q_x q_z - q_w q_y) & 2(q_y q_z + q_w q_x) & 1 - 2(q_x^2 + q_y^2) & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$
##### Components from matrix
If $q_{w}$ is the largest component than we get:
$$
q_w = \frac{1}{2} \sqrt{\operatorname{tr}(\mathbf{M}^{\mathbf{q}})}, \quad
q_x = \frac{m^{\mathbf{q}}_{21} - m^{\mathbf{q}}_{12}}{4 q_w},
$$
$$
q_y = \frac{m^{\mathbf{q}}_{02} - m^{\mathbf{q}}_{20}}{4 q_w}, \quad
q_z = \frac{m^{\mathbf{q}}_{10} - m^{\mathbf{q}}_{01}}{4 q_w}.
$$
Otherwise, we can use the following:
$$
4q_x^2 = +m_{00} - m_{11} - m_{22} + m_{33},
$$
$$
4q_y^2 = -m_{00} + m_{11} - m_{22} + m_{33},
$$
$$
4q_z^2 = -m_{00} - m_{11} + m_{22} + m_{33},
$$
$$
4q_w^2 = \operatorname{tr}(\mathbf{M}^{\mathbf{q}}).
$$
to compute the largest of these components, and then use:
$$
m^{\mathbf{q}}_{21} - m^{\mathbf{q}}_{12} = 4 q_w q_x,
$$
$$
m^{\mathbf{q}}_{02} - m^{\mathbf{q}}_{20} = 4 q_w q_y,
$$
$$
m^{\mathbf{q}}_{10} - m^{\mathbf{q}}_{01} = 4 q_w q_z.
$$
to calculate the remaining components.
##### Spherical Linear Interpolation
Spherical linear interpolation, given two quaternions, and a parameter, computes interpolated quaternion.
$$
\hat{\mathbf{s}}(\hat{\mathbf{q}},\hat{\mathbf{r}},t) = slerp(\hat{\mathbf{q}}, \hat{\mathbf{r}}, t) = \frac{\sin(\phi(1-t))}{\sin \phi}\hat{\mathbf{q}} + \frac{\sin(\phi t)}{\sin \phi}
$$
When combining more quaternions, interpolating them normally yields, bad result. For that reason we can introduce, two new quaternions $\hat{\mathbf{a}}_{i}, \hat{\mathbf{a}}_{i+1}$ between $\hat{\mathbf{q}}_{i}, \hat{\mathbf{q}}_{i+1}$. Spherical cubic interpolation can be defined this set of quaternions.
$$
\hat{\mathbf{a}}_{i} = \hat{\mathbf{q}}_{i} \exp\left[ -\frac{\log( \hat{\mathbf{q}}^{-1}_{i} \hat{\mathbf{q}}_{i-1}) + \log(\hat{\mathbf{q}}^{-1}_{i} \hat{\mathbf{q}}_{i+1})}{4} \right]
$$
The $\hat{\mathbf{q}}_{i} \ \text{and} \ \hat{\mathbf{a}}_{i}$ will be used to spherically interpolate the quaternions using smooth cubic spline.
##### Rotation from one vector to another
To rotate vector $\mathbf{s}$ to vector $\mathbf{t}$, first normalize them, and then compute unit rotation axis $\mathbf{u}$. 
$$
\mathbf{u} = \frac{\mathbf{s} \times \mathbf{t}}{||\mathbf{s} \times \mathbf{t}||}
$$
$$
e = \mathbf{s} \cdot \mathbf{t} = \cos(2\phi)
$$
$$
||\mathbf{s} \times \mathbf{t}|| = \sin(2\phi)
$$
where $2\phi$ is the angle between $\mathbf{s}$ and $\mathbf{t}$.
$$
\hat{\mathbf{q}} = (\mathbf{q}_{v}, \mathbf{q}_{w}) = \left( \frac{1}{\sqrt{2(1+e)}}(\mathbf{s} \times \mathbf{t}), \ \frac{\sqrt{ 2(1+e) }}{2} \right)
$$
###### Matrix representation

$$
\begin{array}
\mathbf{v} & = & \mathbf{s} \times \mathbf{t} \\
e & = & \mathbf{s} \cdot \mathbf{t} \\
h & = & \frac{1}{1+e}
\end{array}
$$
$$
\mathbf{R}(\mathbf{s}, t) =
\begin{pmatrix}
e + h v_x^2 & h v_x v_y - v_z & h v_x v_z + v_y & 0 \\
h v_x v_y + v_z & e + h v_y^2 & h v_y v_z - v_x & 0 \\
h v_x v_z - v_y & h v_y v_z + v_x & e + h v_z^2 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
$$

## Vertex Blending
Let $\mathbf{p}$ be the original vertex and $\mathbf{u}(t)$, the transformed vertex.
$$
\mathbf{u}(t) = \sum_{i=0}^{n-1}w_{i}\mathbf{B}_{i}(t)\mathbf{M}_{i}^{-1}\mathbf{p}, \ \text{where} \sum_{i=0}^{n-1}w_{i} = 1
$$
$w_{i}$ are weights of the bones, $\mathbf{M}_{i}$ is the matrix that transforms bone coordinate system to the world coordinate system. The $\mathbf{B}_{i}$ matrix is the bone world transform, that changes over time.
