Rendering is a process that takes as inputs a set of objects and produces an array of pixels. It can be organized in 2 ways

- Object-order rendering: Where the objects are processed one by one
- Image-order rendering: Where the pixels are processed one by one

Ray tracing is an image-order algorithm

## Basic Algorithm
A basic ray tracer consists of three parts 

- ^^Ray generation^^ : Computes origin and direction of each pixel's viewing ray based on camera geometry
- ^^Ray intersection^^ : Finds the intersection of the viewing ray with the scene geometry
- ^^Lighting^^ : Computes the color of the pixel based on the result of ray-object intersection

```
for each pixel in the image:
    compute viewing ray
    find first object hit by the ray and its surface normal n
    shade the pixel using hit-point, light and n
```

## Ray Generation or Computing Viewing Ray
- basic tools for ray generation are the viewpoint and the image plane
- Ray representation $p(t) = e + t (s - e)$, where $e$ is eye and $s$ is a point on the image plane
- Point $e$ is ray's origin and (s - e) is ray's direction

<figure markdown="span">
   ![Ray Generation](images/ray_generation.png){ width="400" } 
  <figcaption>Ray Generation</figcaption>
</figure>

- Ray generation takes place from the camera frame
- position $e$ (eye point)
- $\mathbf{u},  \mathbf{v},  \mathbf{w}$ are basis vectors
- Choose $-w$ as view direction and an up vector, using which we construct the basis vectors

<figure markdown="span">
    ![Camera Vectors](images/camera_vectors.png){ width="400" }
    <figcaption>Camera Vectors</figcaption>
</figure>

### Orthographic Views

- All rays will have direction $- \mathbf{w}$
- A viewpoint is not require but viewing rays can start from the plane containing the camera, so we know when object is behind the camera.
- Viewing rays start on the image plane and are parallel to each other, and cab be defined by point $e$ and vectors $\mathbf{u}$ and $\mathbf{v}$

<figure markdown="span">
    ![Orthographic Rays](images/orthographic_rays.png){ width="300" }
    <figcaption>Orthographic Rays</figcaption>
</figure>

- $l$ and $r$ are left and right limits of the image plane (measured along $\mathbf{u}$) $l < 0 < r$
- $b$ and $t$ are bottom and top limits of the image plane (measured along $\mathbf{v}$) $b < 0 < t$

Pixel spacing for $n_x \times n_y$ image is

- Horizontal : $\Large \frac{r - l}{n_x}$
- Vertical : $\Large \frac{t - b}{n_y}$

Therefore, pixel position $(i, j)$ in the raster image is 

- $u = l + \Large \frac{(r - l)(i + 0.5)}{n_x}$
- $v = b + \Large \frac{(t - b)(j + 0.5)}{n_y}$

Where $u, v$ are the coordinates of the pixel in the image plane w.r.t origin $e$ and basis vectors $\mathbf{u} ,  \mathbf{v}$

Therefore, Ray parameters are 

- Origin: $e + u * \mathbf{u} + v * \mathbf{v}$
- Direction : $-\mathbf{w}$

### Perspective Views

- All rays will have different directions for different pixels
- All rays will have origin at the eye point

<figure markdown="span">
    ![Perspective Rays](images/perspective_rays.png){ width="500" }
    <figcaption>Perspective Rays</figcaption>
</figure>

- Image plane positioned at distance $d$ from the eye point $e$
- Ray parameters are 
    - Origin: $e$
    - Direction: $-d * \mathbf{w} + u * \mathbf{u} + v * \mathbf{v}$

Where $u, v$ are the coordinates of the pixel in the image plane w.r.t origin $e$ and basis vectors $\mathbf{u} ,  \mathbf{v}$  

!!! note 
    In some sense, the origin in orthographic view is direction in perspective view.


## Ray intersection

- Given a generated ray $p(t) = e + t \cdot d$, find intersection (first hit) with the scene geometry such that $t > 0$
- Given a ray $p(t) = e + t \cdot d$, and an implicit surface $f(p) = 0$, the intersection point is found by solving $f(e + t \cdot d) = 0$ 
- There can be multiple solutions for $t$, but we are interested in the smallest positive solution

### For Sphere

- Parametric equation for any point $p$ on a sphere with center $c$ and radius $r$ is 

$$ (p - c) \cdot (p - c) - r^2 = 0 $$

- For finding points of intersection of a ray with a sphere, we substitute $p = e + t \cdot d$ in the above equation and solve for $t$

$$
\begin{align*}
    (e + t \cdot d - c) \cdot (e + t \cdot d - c) - r^2 &= 0 \\
    (d \cdot d) t^2 + 2 (d \cdot (e - c)) t + (e - c) \cdot (e - c) - r^2 &= 0
\end{align*}
$$

This gives the solution

$$t = \frac {-(d \cdot (e - c)) \pm \sqrt{(d \cdot (e - c))^2 - (d \cdot d) ((e - c) \cdot (e - c) - r^2)}}{d \cdot d}$$

#### Normal for Sphere
- The normal vector at $\mathbf{p}$ on the implicit surface $f(p)$ is given by 

$$n = \nabla f(p) = (\frac{\partial f(p)}{\partial x}, \frac{\partial f(p)}{\partial y}, \frac{\partial f(p)}{\partial z})$$


- For sphere, the normal at point $p$ is

$$n = 2(p - c) \hspace{20px} \text{and} \hspace{20px} \hat{n} = \frac{p - c}{R}$$


### For Triangle 

- Parametric equation for a triangle is

$$\mathbf{e} + t \mathbf{d} = \mathbf{f}(u, v)$$ 

- 3 unknowns $t, u, v$ and 3 equations $(x, y, z)$ for the triangle. We can solve for $t, u, v$ and check if $u, v$ are within the range of the triangle.

- For a parametric plane, the parametric surface can be represented in terms of any three points in the plane. Utilize barycentric coordinates for ray-triangle test 

- For a triangle with vertices $\mathbf{a},  \mathbf{b}, \mathbf{c}$ intersection will occur when 

$$\mathbf{e} + \mathbf{d} t = \mathbf{a} + \beta (\mathbf{b} - \mathbf{a}) + \gamma (\mathbf{c} - \mathbf{a})$$ 

- Intersection is inside the triangle if $\beta, \gamma \geq 0$ and $\beta + \gamma \leq 1$
- To solve for $t, \beta, \gamma$, we can write the above equation as

$$
\begin{align*}
    x_e + t x_d &= x_a + \beta (x_b - x_a) + \gamma (x_c - x_a) \\
    y_e + t y_d &= y_a + \beta (y_b - y_a) + \gamma (y_c - y_a) \\
    z_e + t z_d &= z_a + \beta (z_b - z_a) + \gamma (z_c - z_a)
\end{align*}
$$

This can be written in matrix form as

$$
\begin{bmatrix}
    x_a - x_b & x_a - x_c & x_d \\
    y_a - y_b & y_a - y_c & y_d \\
    z_a - z_b & z_a - z_c & z_d
\end{bmatrix}
\begin{bmatrix}
    \beta \\
    \gamma \\
    t
\end{bmatrix}
= 
\begin{bmatrix}
    x_a - x_e \\
    y_a - y_e \\
    z_a - z_e
\end{bmatrix}
$$

- Let $A$ be the matrix on the left, $B$ be the matrix on the right, then using Cramer's rule, we can solve for $\beta, \gamma, t$ as follows

- Let $A_i$ be the matrix obtained by replacing $i^{th}$ column of $A$ with the column of $B$, then values of $\beta, \gamma, t$ are

$$
\beta = \frac{\text{det}(A_1)}{\text{det}(A)} \hspace{20px} \gamma = \frac{\text{det}(A_2)}{\text{det}(A)} \hspace{20px} t = \frac{\text{det}(A_3)}{\text{det}(A)}
$$

### Ray-Polygon Intersection

Given $m$ vertices $p_1, p_2, \ldots, p_m$ of a polygon and surface normal $n$
- Compute the intersection point between ray $\mathbf{e} + t \mathbf{d}$ and the plane containing the polygon $(p - p_1) \cdot n = 0$

$$t = \frac{(p_1 - e) \cdot n}{d \cdot n}$$

- If $\mathbf{p}$ is inside the polygon, then the ray hits it.

## Point-in-Polygon Test

### Ray Polygon Intersection or Crossing Number Algorithm

- Send a 2D ray out from $p$ and count the number of intersections between the ray and the polygon
- If the intersection count is odd, then $p$ is inside the polygon

!!! Warning
    It's a ray, so only one way

- Easily done by checking the sign of the cross product of the vectors from $p$ to the vertices of the polygon

<figure markdown="span">
    ![Crossing Number Algorithm](images/crossing_number_algo.svg){ width="400" }
    <figcaption>Crossing Number Algorithm</figcaption>
</figure>

### Winding Number Algorithm

- Winding number of a closed curve in the plane around a given point is an integer representing the total number of times that curve travels counterclockwise around the point
- If the winding number is non-zero, then the point is inside the polygon

<figure markdown="span">
    ![Winding Number Algorithm](images/winding_number_algo.png){ width="400" }
    <figcaption>Winding Number Algorithm</figcaption>
</figure>

## Shading and Lighting

### Intersection with Multiple Objects

Typically, a scene will contain multiple objects. To find the first object hit by the ray, we need to find the smallest positive $t$ value

```python
t_min = infinity
firstSurface = None
for each object in the surfaceList:
    hitSurface, t = object.intersect(ray)
    if hitSurface != None and t < t_min:
        t_min = t
        firstSurface = hitSurface

return firstSurface, t_min
```

### Shading 

We have already read about the Phong reflection model in the [Lighting](lighting.md#phong-reflection-model) section. We can use the same model to shade the pixel, so our algorithm becomes as follows

```python
def Scene::trace(ray, t_min, t_max):
    surface, t = surfaces.intersect(ray, t_min, t_max)
    if surface == None:
        return background_color
    else:
        return surface.shade(ray, t, light)

def Surface::shade(ray, t, light):
    p = ray.origin + t * ray.direction
    n = surface_normal(p)
    v = normalize(ray.origin - p)
    l = normalize(light.position - p)
    h = normalize(v + l)
    # compute ambient, diffuse and specular components
```

The shading algorithm can be changed for multiple light sources as well

### Casting Shadows

- Surface is illuminated if nothing blocks the view of the light source
- To check if a point is in shadow, we can cast a ray from the point to the light source 
    and check if it intersects any object
- As many rays need to be cast as there are light sources
- Ideally test $t \in [0, \infty]$, but to account for floating point errors, test $t \in [0 + \epsilon, \infty]$ where $\epsilon$ is a small positive number

```python
def Surface::shade(ray, t, lights):
    p = ray.origin + t * ray.direction
    n = surface_normal(p)
    v = normalize(ray.origin - p)
    for each light in lights:
        l = normalize(light.position - p)
        h = normalize(v + l)
        shadowRay = Ray(p, l)
        if inShadow(shadowRay):
            # point is in shadow
            return ambient
        else:
            # compute ambient, diffuse and specular components
            return shading
```

### Specular Reflections
- Mirror reflections can be added by shading reflected rays $r = d - 2(d \cdot n)n$
- Some energy is lost in each reflection, so we can recursively 
  
$$ c = c + k_m \text{raycolor}(p + tr, \epsilon, \infty)$$

- $k_m$ is specular RGB color for mirror reflection
- Trace reflected rays for materials that are specular
- Recursion depth can be limited to avoid infinite recursion

### Refraction and Transparency

- Compute refracted ray as following

$$t = \frac{n_1}{n_2} (d - (d \cdot n)n) - n \sqrt{1 - (\frac{n_1}{n_2})^2 (1 - (d \cdot n)^2)}$$

#### Total Internal Reflection

- Happens when light travels from denser to rarer medium at an angle greater than the critical angle
- Critical angle $\cos (\theta_c) = \frac{n_2}{n_1}$

#### Schlick's Approximation

- Approximates the Fresnel equations for reflection and refraction

$$R = R_0 + (1 - R_0) (1 - \cos \theta)^5, \hspace{20px} R_0 = \left( \frac{n_1 - n_2}{n_1 + n_2} \right)^2$$

#### Beer's Law

- For homogeneous impurities in a dielectric, a light carrying ray's intensity attenuates as per Beer's law
- Loss of intensity in the medium $dI = -C I dx$
- Solution: $I = k' + k e^{-C x}$ with boundary conditions $I(s) = I_0 e^{s\ln(a)}$
- $s$ is distance from interface, and $a$ is attenuation constant

### Putting it all together

```python
def Surface::shade(ray, point, normal, lights):
    if point is on a dielectric:
        r = reflect(ray, normal)
        if dot(ray, normal) < 0: # entering a dielectric
            c = -dot(ray, normal)
            k_r = k_g = k_b = 1
        else:
            # apply Beer's law
            k_r = expo(-a_r * t)
            k_g = expo(-a_g * t)
            k_b = expo(-a_b * t)

            if refract(ray, -normal, 1/eta, t):
                c = dot(t, normal)
            else:
                return k * Scene::trace(r, point, epsilon, infinity)
        
        R_0 = ((eta - 1) / (eta + 1)) ** 2
        R = R_0 + (1 - R_0) * (1 - c) ** 5
        return k * (
                R * Scene::trace(r, point, epsilon, infinity) + \
                (1 - R) * Scene::trace(t, point, epsilon, infinity)
            )
```

