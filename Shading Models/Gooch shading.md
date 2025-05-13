Simple stylised shading model. Compare the surface normal to the light direction. If the normal is pointing towards the light, use warmer tone for the color, otherwise a cooler tone.
$$
\mathbf{c}_{\text{shaded}} = s \mathbf{c}_{\text{hightlight}} + (1-s)t \mathbf{c}_{\text{warm}} + (1-t) \mathbf{c}_{\text{cool}}
$$
$$
\begin{array}{lml}
\mathbf{c}_{\text{cool}}& = &(0, 0, 0.55) + 0.25 \mathbf{c}_{\text{surface}} \\
\mathbf{c}_{\text{warm}}& = &(0.3, 0.3, 0.0) + 0.25 \mathbf{c}_{\text{surface}} \\
\mathbf{c}_{\text{highlight}} &=& (1, 1, 1) \\
t &=& \frac{(\mathbf{n} \cdot \mathbf{l}) + 1}{2} \\
\mathbf{r} &=& 2(\mathbf{n} \cdot \mathbf{l})\mathbf{n} - \mathbf{l} \\
s &=& 100(\mathbf{r} \cdot \mathbf{v}) - 97^{\mp}
\end{array}
$$
