!!! note
    Please read about [Curves](curves.md) before reading this article.

## Re-Parametrization of Curves

Given a function $f(u), u \in [a, b]$, defining another function $f_2(u) = f(g(u))$ is called re-parametrization of $f$, where $g: \mathbb{R} \rightarrow \mathbb{R}$.

For example, for a curve $f$ with parameter $u \in [0, 1]$,

- $(x, y) = f(u) = (u, u)$
- $(x, y) = f(u) = (u^2, u^2)$
- $(x, y) = f(u) = (u^5, u^5)$

They all represent the same curve but with different speeds.

## Arc-Length Parametrization

Arc-length distance along a curve from point $f(0)$ to $f(v)$:

$$ s = \int_o^v \left|\frac{df(t)}{dt}\right| dt $$

$s$ could be used as a natural parameterization for $f$. For $f(s)$, the magnitude of tangent is constant, i.e. $|df(s)/ds| = 1$.

## Curve Representations

A polynomial function has the form $f(t) = a_0 + a_1 t + a_2 t^2 + ... + a_n t^n, a_n \neq 0$. where $a_i$ are coefficients and $n$ is the degree of the polynomial. Cannonical form of a polynomial curve becomes $f(t) = \sum_{i=0}^n a_i t^i$, but this can be generalized to

$$f(t) = \sum_{i=0}^n c_i B_i(t)$$

where $B_i(t)$ is a polynomial basis function.

### Line Segment

Line segment connection $\mathbf{p}_0$ and $\mathbf{p}_1$

$$
\begin{align*}
f(u) &= \mathbf{p}_0 + u(\mathbf{p}_1 - \mathbf{p}_0) \\
&= \mathbf{a}_0 + u\mathbf{a}_i \\
&= \mathbf{u} \cdot \mathbf{a}
\end{align*}
$$

Here, $\mathbf{u} = [1, u]$ and $\mathbf{a} = [\mathbf{a}_0, \mathbf{a}_1]$. In general, we can write

$$
\begin{align*}
\mathbf{p}_0 &= f(0) = \begin{bmatrix} 1 & 0 \end{bmatrix} \cdot \begin{bmatrix} \mathbf{a}_0 & \mathbf{a}_1 \end{bmatrix}^\top \\
\mathbf{p}_1 &= f(1) = \begin{bmatrix} 1 & 1 \end{bmatrix} \cdot \begin{bmatrix} \mathbf{a}_0 & \mathbf{a}_1 \end{bmatrix}^\top
\end{align*}
$$

In matrix form, it becomes 

$$\begin{bmatrix} \mathbf{p}_0 & \mathbf{p}_1 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 1 & 1 \end{bmatrix} \cdot \begin{bmatrix} \mathbf{a}_0 & \mathbf{a}_1 \end{bmatrix}^\top \implies \mathbf{p} = \mathbf{C} \cdot \mathbf{a}$$

Where $\mathbf{C}$ is the constraint matrix, and $\mathbf{a}$ are unknown coefficients. Inversion of $\mathbf{C}$ gives $f(u) = \mathbf{u} \mathbf{B} \mathbf{p}$, where $\mathbf{B} = \mathbf{C}^{-1}$.

### Quadratic Curves

Same cannonical form applies by letting $n = 2$. $\mathbf{B}$ is a $3 \times 3$ matrix, obtained by solving a linear system of positional constraints. Constraints on derivatives can be applied as well

$$
\begin{align*}
f(u) = \mathbf{a}_0 + u\mathbf{a}_1 + u^2\mathbf{a}_2 \\
f'(u) = \frac{df(u)}{du} = \mathbf{a}_1 + 2u\mathbf{a}_2 \\
f''(u) = \frac{d^2f(u)}{du^2} = 2\mathbf{a}_2
\end{align*}
$$

Which produces $C = \begin{bmatrix} 1 & u & u^2 \\ 0 & 1 & 2u \\ 0 & 0 & 2 \end{bmatrix}$

### Cubic Curves

Same idea, but now we have 4 constraints. Hermite form is where positional and first derivative constraints are imposed as first ($u = 0$) and last points ($u = 1$). Let's work it out through one example.

- $p_0 = f(0)$
- $p_1 = f'(0)$
- $p_2 = f(1)$
- $p_3 = f'(1)$

Now we know that $\mathbf{p} = \mathbf{C} \cdot \mathbf{a}$ where $\mathbf{C}$ is our constraint matrix and $\mathbf{a}$ is the unknown coefficients. We will consider each constraint one by one.

- $p_0 = f(0) = a_0 \implies$ first row of $\mathbf{C}$ is $[1, 0, 0, 0]$
- $p_1 = f'(0) = a_1 \implies$ second row of $\mathbf{C}$ is $[0, 1, 0, 0]$
- $p_2 = f(1) = a_0 + a_1 + a_2 + a_3 \implies$ third row of $\mathbf{C}$ is $[1, 1, 1, 1]$
- $p_3 = f'(1) = a_1 + 2a_2 + 3a_3 \implies$ fourth row of $\mathbf{C}$ is $[0, 1, 2, 3]$

So our matrix $\mathbf{C}$ becomes

$$\mathbf{C} = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 1 & 1 & 1 & 1 \\ 0 & 1 & 2 & 3 \end{bmatrix}$$

Inverting this, we get $\mathbf{B} = \mathbf{C}^{-1}$, and our curve becomes $f(u) = \mathbf{u} \mathbf{B} \mathbf{p}$.

### Blending Functions

Define a vector of functions $\mathbf{b}(u) = \mathbf{u} \mathbf{B}$, where elements of $\mathbf{b}(u)$ are blending functions. The control points can be blended linearly with these functions to get the curve

$$f(u) = \sum_{i=0}^n \mathbf{b}_i(u) \mathbf{p}_i$$

## Piecewise Polynomial Curves

$$f(u) = \begin{cases} f_1(2u) & u \in [0, 0.5] \\ f_2(2u-1) & u \in [0.5, 1] \end{cases}$$

where $f_1$ and $f_2$ are functions for each of the two line segments. 
These curves are only $C^0$ continuous, i.e. they are continuous but not smooth.

we can also write piecewise polynomials as a weighted sum of basis functions

$$f(u) = p_1 b_1(u) + p_2 b_2(u) + p_3 b_3(u)$$

#### Knots

In a piecewise function, _knots_ are sites where pieces begins or ends. We can represent the knots by their $u$ values, and store them in a vector in ascending order. Such a vector is called a _Knot vector_

## Cubics

They allow for $C^2$ continuity, which is considered suitable for most visual tasks. They provide a minimum-curvature interpolants to a set of points

| Desirable Property | B-Splines | Catmull-Rom | Cardinal | Natural Cubics |
|--------------------|-----------|-------------|----------|---------------|
| Piece-wise cubic | Yes | Yes | Yes | Yes |
| Interpolating curve | No | Yes | Yes | Yes |
| Curve has local control | Yes | Yes | Yes | No |
| Curve has $C^2$ continuity | Yes | No | No | Yes |

Can only satisfy 3 of the 4 properties at a time.

### Natural Cubic Splines

For one segment, parameterized by the positions on it's end-points, and the first and second derivative at the beginning point

- $p_0 = f(0)$
- $p_1 = f'(0)$
- $p_2 = f''(0)$
- $p_3 = f(1)$

The constraint matrix $\mathbf{C}$ becomes $\begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 2 & 0 \\ 1 & 1 & 1 & 1 \end{bmatrix}$

### Hermite Cubics

For one segment, parameterized by the positions on it's end-points, and the first derivative at end-points 

- $p_0 = f(0)$
- $p_1 = f'(0)$
- $p_2 = f(1)$
- $p_3 = f'(1)$

We did this earlier, refer to the polynomial section for the constraint matrix.

### Cardinal Cubic Splines

Interpolates all but the first and last points. Tension parameter controls the tightness of the curve. For $t = 0$, it becomes a Catmull-Rom spline. It's local, but only $C^1$ continuous.

Each segment uses 4 control points $i, i+1, i+2, i+3$. Segment begins at second point $p_1$ and ends at third point $p_2$. Derivative at $p_1$ is proportional to vector $p_2 - p_0$ and derivative at $p_2$ is proportional to $p_3 - p_1$. 


- $f(0) = p_1$
- $f(1) = p_2$
- $f'(0) = \frac{1}{2}(1 - t)(p_2 - p_0)$
- $f'(1) = \frac{1}{2}(1 - t)(p_3 - p_1)$

Solving this to find $p_0$ and $p_3$, we get

- $p_0 = f(1) - \frac{2}{1-t}f'(0)$
- $p_1 = f(0)$
- $p_2 = f(1)$
- $p_3 = f(0) + \frac{2}{1-t}f'(1)$

!!! note

    Do work out the matrix $\mathbf{C}$ for this case.

## Approximating Curves

Curves which donot pass through the control points are called _approximating curves_. 

### Bezier Curves

We have already studied bezier curves, but let's use polynomial representation to understand them better.

- $p_0 = f(0)$
- $p_3 = f(1)$
- $3(p_1 - p_0) = f'(0)$
- $3(p_3 - p_2) = f'(1)$

Rewriting it in terms of blending functions, we get 

$$f(u) = \sum_{i=0}^3 \mathbf{b}_i(u) \mathbf{p}_i$$

with blending functions $\mathbf{b}_i(u) = \binom{3}{i} u^i (1-u)^{3-i}$. These blending functions are also called _Bernstein polynomials_.

A way to evaluate the curve is to use _de Casteljau's algorithm_.

> Subdivide each line segment of the control polyline in the ratio t:(1-t) and join to create new poly line. Continue until only 1 point is left.This point lies on the Bézier curve at parameter t.

<figure markdown="span">
    ![De Casteljau's Algorithm](images/Bezier_cubic_anim.gif)
    <figcaption>De Casteljau's Algorithm</figcaption>
</figure>

### B-Splines

Approximating a set of $n$ points with a polynomial of degree $d$ that gives $C^{d-1}$ continuity. Generally, 

$$f(t) = \sum_{i = 1}^n \mathbf{b}_i(t) \mathbf{p}_i$$

where $\mathbf{b}_i(t)$ are blending functions. The curve is defined by a set of control points $\mathbf{p}_i$ and a set of blending functions $\mathbf{b}_i(t)$. The blending functions are defined by a set of knots $t_i$.

### Uniform linear B-Splines

$$b_{i, 2} = \begin{cases} t - i & i \leq t < i+1 \\ 
2 - t + i & i+1 \leq t < i+2 \\ 0 & \text{otherwise} \end{cases}$$

### Uniform Quadratic B-Splines

$$b_{i, 3} = \begin{cases} \frac{1}{2}(t - i)^2 & i \leq t < i+1 \\
\frac{1}{2} + (t - i)(2 - t + i) & i+1 \leq t < i+2 \\
\frac{1}{2}(2 - t + i)^2 & i+2 \leq t < i+3 \\ 0 & \text{otherwise} \end{cases}$$

### Non-Uniform B-Splines

B-splines are defined for any non-decreasing knot vector $\mathbf{t}$, which not necessarily be Uniform. Non-uniform knot-spacing actually gives more control over the shape of the curve.
