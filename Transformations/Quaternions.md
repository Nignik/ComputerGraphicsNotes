## Definitions
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
## Useful Equations
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
## Quaternion Transformations
#### Rotations
$\hat{\mathbf{q}}\hat{\mathbf{p}}\hat{\mathbf{q}}^{-1}$ rotates $\hat{\mathbf{p}}$ around the axis $\mathbf{u}_{q}$ by angle $2\phi$.
Given two unit quaternions $\hat{\mathbf{q}}, \ \hat{\mathbf{r}}$ the concatenation of first applying $\hat{\mathbf{q}}$ is:
$$
\hat{\mathbf{r}} (\hat{\mathbf{q}} \hat{\mathbf{p}} \hat{\mathbf{q}}^*) \hat{\mathbf{r}}^* = (\hat{\mathbf{r}} \hat{\mathbf{q}}) \hat{\mathbf{p}} (\hat{\mathbf{r}} \hat{\mathbf{q}})^* = \hat{\mathbf{c}} \hat{\mathbf{p}} \hat{\mathbf{c}}^*, \ \text{where} \ \hat{\mathbf{c}} = \hat{\mathbf{r}}\hat{\mathbf{q}}
$$
#### Quaternion rotation as a matrix
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
#### Components from matrix
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
#### Spherical Linear Interpolation
Spherical linear interpolation, given two quaternions, and a parameter, computes interpolated quaternion.
$$
\hat{\mathbf{s}}(\hat{\mathbf{q}},\hat{\mathbf{r}},t) = slerp(\hat{\mathbf{q}}, \hat{\mathbf{r}}, t) = \frac{\sin(\phi(1-t))}{\sin \phi}\hat{\mathbf{q}} + \frac{\sin(\phi t)}{\sin \phi}
$$
When combining more quaternions, interpolating them normally yields, bad result. For that reason we can introduce, two new quaternions $\hat{\mathbf{a}}_{i}, \hat{\mathbf{a}}_{i+1}$ between $\hat{\mathbf{q}}_{i}, \hat{\mathbf{q}}_{i+1}$. Spherical cubic interpolation can be defined this set of quaternions.
$$
\hat{\mathbf{a}}_{i} = \hat{\mathbf{q}}_{i} \exp\left[ -\frac{\log( \hat{\mathbf{q}}^{-1}_{i} \hat{\mathbf{q}}_{i-1}) + \log(\hat{\mathbf{q}}^{-1}_{i} \hat{\mathbf{q}}_{i+1})}{4} \right]
$$
The $\hat{\mathbf{q}}_{i} \ \text{and} \ \hat{\mathbf{a}}_{i}$ will be used to spherically interpolate the quaternions using smooth cubic spline.
#### Rotation from one vector to another
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
##### Matrix representation

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