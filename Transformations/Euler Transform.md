## Formula
$$
\mathbf{E}(h, p, r) = \mathbf{R}_{z}(r)\mathbf{R}_{x}(p)\mathbf{R}_{y}(h)
$$
$$
\mathbf{E}^{-1} = \mathbf{E}^T
$$
_head_: y-roll, yaw
_pitch_: x-roll
_roll_: z-roll

## Extracting Parameters
$$
\begin{array}{lcl}
h & = & \text{atan}2(-e_{20}, e_{22}) \\
p & = & \arcsin(e_{21}) \\
r & = & \text{atan}2(-e_{01}, e_{11})
\end{array}
$$
## Rotation Around Arbitrary Axis
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