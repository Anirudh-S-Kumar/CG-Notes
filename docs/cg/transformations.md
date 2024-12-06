Transformations are very fundamental in computer graphics. They are used for Object Modelling, Viewing, and Projection. 

Objects in a scene are a collection on points which have some location, orientation and size. These properties can be changed by Translations($\mathbf{T}$), Rotations($\mathbf{R}$), and Scaling ($\mathbf{S}$).

## Homogeneous Coordinates
We can represent Rotation and Scaling as 2x2 matrices, but we cannot do so for Translation. There is non-linearity in Translation. To make Translation linear, we use Homogeneous Coordinates. This allows us to represent all 3 2D transformations as 3x3 matrices.

??? info "Proof that translation is non-linear"
    Let $\mathbf{T}(p) = p + t$ be the translation of point $p$ by vector $t$. Then,

    $$\mathbf{T}(p + q) = p + q + t \neq \mathbf{T}(p) + \mathbf{T}(q)$$

    $$\mathbf{T}(ap) = ap + t \neq a\mathbf{T}(p)$$

    Hence, Translation is non-linear.

To convert a point $(x, y)$ to Homogeneous Coordinates, we do the following:

$$\begin{bmatrix}x\\y\end{bmatrix} \rightarrow \begin{bmatrix}wx\\wy\\w\end{bmatrix}, w \neq 0$$

where $w$ is a scaling factor. We can convert back to Cartesian Coordinates by dividing by $w$. For linear transformations, embed the 2x2 matrix in a 3x3 matrix by adding a row and a column of 0s and a 1 in the bottom right corner.

$$\begin{bmatrix}a & b\\c & d\end{bmatrix} \rightarrow \begin{bmatrix}a & b & 0\\c & d & 0\\0 & 0 & 1\end{bmatrix}$$

## 2D Transformations in Homogeneous Coordinates

<div class="center-table" markdown>

| Transformation | Matrix |
|----------------|--------|
| Translation    | $\begin{bmatrix}1 & 0 & t_x\\0 & 1 & t_y\\0 & 0 & 1\end{bmatrix}$ |
| Rotation       | $\begin{bmatrix}\cos\theta & -\sin\theta & 0\\\sin\theta & \cos\theta & 0\\0 & 0 & 1\end{bmatrix}$ |
| Scaling        | $\begin{bmatrix}s_x & 0 & 0\\0 & s_y & 0\\0 & 0 & 1\end{bmatrix}$ |
| $\text{Shear}_x$ ($\phi$ is angle along axis)      | $\begin{bmatrix}1 & \tan{\phi} & 0\\0 & 1 & 0\\0 & 0 & 1\end{bmatrix}$ |
| $\text{Shear}_y$       | $\begin{bmatrix}1 & 0 & 0\\ \tan{\phi} & 1 & 0\\0 & 0 & 1\end{bmatrix}$ |

</div>

!!! info "Properties of Rotation Matrix"
    - Rows are orthogonal to each other
    - Columns are orthogonal to each other
    - $\mathbf{R}^\top = \mathbf{R}^{-1}$
    - $\det(\mathbf{R}) = 1$

    Make sure these are always satisfied.



## Composition of Transformations
To apply multiple transformations to a point, we multiply the matrices of the transformations. The order of multiplication is important. For example, to rotate and then translate a point, we would do $\mathbf{T}\mathbf{R}p$. Operations are evaluated from right to left.

!!! warning "Order of Multiplication"
    In general, Matrix Multiplication is not commutative. $\mathbf{AB} \neq \mathbf{BA}$.

### Transformation about Arbitrary Point
To rotate a point about an arbitrary point $(p_x, p_y)$, we first translate the point to the origin, rotate it, and then translate it back.

$$ \mathbf{R}_p(\phi) = \mathbf{T}(p_x, p_y) \hspace{10px} \mathbf{R}(\phi) \hspace{10px} \mathbf{T}(-p_x, -p_y) $$

Similarly for scaling, we can perform the following:

$$ \mathbf{S}_p(s_x, s_y) = \mathbf{T}(p_x, p_y) \hspace{10px} \mathbf{S}(s_x, s_y) \hspace{10px} \mathbf{T}(-p_x, -p_y) $$

## Decomposition of Transformations

Any 2D matrix can be decomposed into a product of rotation, scale, rotation. 

- Eigenvalue Decomposition: $\mathbf{A} = \mathbf{R} \hspace{10px} \mathbf{S} \hspace{10px} \mathbf{R}^{\top}$ 

!!! note
    Eigenvalue Decomposition only works for symmetric matrices.

!!! info Interpreting the Decomposition
    - $\mathbf{R}^{\top}$: Rotate the object to X and Y axes.
    - $\mathbf{S}$: Scale the object.
    - $\mathbf{R}$: Rotate the object back to its original orientation.

    In a way it's directional scaling.

- SVD Decomposition: $\mathbf{A} = \mathbf{U} \hspace{10px} \mathbf{S} \hspace{10px} \mathbf{V}^{\top}$

- Paeth Decomposition: Applies only to rotations. Uses shear to represent non-zero rotations. Very useful in raster image rotations.

$$ \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix} = \begin{bmatrix} 1 & \frac{\cos \phi - 1}{\sin \phi} \\ 0 & 1 \end{bmatrix} \begin{bmatrix} 1 & 0 \\ \sin \phi & 1 \end{bmatrix} \begin{bmatrix} 1 & \frac{ \cos \phi - 1}{\sin \phi} \\ 0 & 1 \end{bmatrix} $$

## 3D Transformations

Properties which were applicable in 2D transformations are also applicable in 3D transformations. The only difference is that we have an additional axis.

<div class="center-table" markdown>

| Transformation | Matrix |
|----------------|--------|
| Translation    | $\begin{bmatrix}1 & 0 & 0 & t_x\\0 & 1 & 0 & t_y\\0 & 0 & 1 & t_z\\0 & 0 & 0 & 1\end{bmatrix}$ |
| Rotation about X-axis       | $\begin{bmatrix}1 & 0 & 0 & 0\\0 & \cos\theta & -\sin\theta & 0\\0 & \sin\theta & \cos\theta & 0\\0 & 0 & 0 & 1\end{bmatrix}$ |
| Rotation about Y-axis       | $\begin{bmatrix}\cos\theta & 0 & \sin\theta & 0\\0 & 1 & 0 & 0\\-\sin\theta & 0 & \cos\theta & 0\\0 & 0 & 0 & 1\end{bmatrix}$ |
| Rotation about Z-axis       | $\begin{bmatrix}\cos\theta & -\sin\theta & 0 & 0\\\sin\theta & \cos\theta & 0 & 0\\0 & 0 & 1 & 0\\0 & 0 & 0 & 1\end{bmatrix}$ |
| Scaling        | $\begin{bmatrix}s_x & 0 & 0 & 0\\0 & s_y & 0 & 0\\0 & 0 & s_z & 0\\0 & 0 & 0 & 1\end{bmatrix}$ |

</div>

### Arbitrary Axis Rotation

Given 3 mutually orthogonal unit vectors $\mathbf{u} = (x_u, y_u, z_u)$, $\mathbf{v} = (x_v, y_v, z_v)$, $\mathbf{w} = (x_w, y_w, z_w)$, $R_{uvw}$ transforms the coordinate system from $xyz$ to $uvw$.

$$ R_{uvw} = \begin{bmatrix} x_u & y_u & z_u \\ x_v & y_v & z_v \\ x_w & y_w & z_w\end{bmatrix} = \begin{bmatrix} u \\ v \\ w \end{bmatrix} $$

To rotate around arbitrary vector $\mathbf{a} = (x_a, y_a, z_a)$

- Form an orthonormal $uvw$ coordinate system with $w = \mathbf{a}$ 
- Rotate $uvw$ basis to canonical basis $xyz$
- Rotate about $z$ axis by $\phi$
- Rotate back to $uvw$ basis

$$R_a(\phi) = R_{uvw}^\top \hspace{10px} R_z(\phi) \hspace{10px} R_{uvw}$$

#### Constructing a basis from a vector

- make $w$ a unit vector $w = \frac{a}{||a||}$
- Choose any vector $t$ not parallel to $w$, and build $u = \frac{t \times w}{||t \times w||}$
- Complete the basis by $v = w \times u$

### Transforming Normals

- Normals are very common in computer graphics, so we need a way to also transform surface normals.
- They do not transform the way surfaces do 
- Let the surface points be transformed by the matrix $\mathbf{M}$. Then the normal vectors are transformed by the the following

$$ \mathbf{N'} = \mathbf{M}^{-\top} \mathbf{N} $$

??? Abstract "Proof of Transforming Normals"

    Say you have a point $p$ and a normal $n$ on a surface. The normal is perpendicular to the surface at that point, i.e.

    $$n^\top p = 0$$

    If we transform the point to $p' = \mathbf{M}p$, then the new normal $n'$ should be perpendicular to the new surface at $p'$, i.e.

    $$n'^\top p' = 0$$

    Let the new normal be $n' = \mathbf{N}n$. Then,

    $$n'^\top p' = (\mathbf{N}n)^\top \mathbf{M}p = n^\top \mathbf{N}^\top \mathbf{M}p = 0 $$

    Since we already know that $n^\top p = 0$, we can say that $\mathbf{N}^\top \mathbf{M} = I$. Hence, $\mathbf{N} = \mathbf{M}^{-\top}$.