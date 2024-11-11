Objects have variation in reflectance across surface. A common technique to handle such variation is to store the reflectance as a function or a pixel-based image and "map" it onto the surface. This function or image is called **Texture**, and the process of controlling reflectance properties of objects using textures is called **Texture Mapping**.

## 2D Texture Mapping
- Local 2D coordinate system called *uv* is used to create reflectance $R(u,v)$.
- During texture mapping, each surface point $(x,y,z)$ is assigned a 2D coordinate $(u,v)$ and colored with $R(u,v)$.


### Texture mapping on sphere

- To map $(u, v)$ onto a sphere, we first compute spherical coordinate
    - $x = x_c + r \sin(\theta) \cos(\phi)$
    - $y = y_c + r \sin(\theta) \sin(\phi)$
    - $z = z_c + r \cos(\theta)$
    - $\theta = arccos(\frac{z - z_c}{r})$
    - $\phi = arctan2(y - y_c, x - x_c)$ 
- Required mapping becomes
    - $u = \frac{\phi + \pi}{2\pi}$
    - $v = \frac{\theta}{\pi}$ 

<figure markdown="span">
    ![Texture mapping on sphere](images/uv_mapping_sphere.png){ width=400}
    <figcaption markdown="span">Texture mapping on sphere</figcaption>
</figure>

### Texture mapping on triangle

- At any point $(\beta, \gamma)$ inside a triangle, the $(u, v)$ coordinates can be computed as
    - $u = = (1 - \beta - \gamma)u_a + \beta u_b + \gamma u_c$
    - $v = = (1 - \beta - \gamma)v_a + \beta v_b + \gamma v_c$
- Here, $(u_a, v_a)$, $(u_b, v_b)$, and $(u_c, v_c)$ are the texture coordinates at the vertices of the triangle.

### Perspective correct texture mapping

- Accounts for the actual 3D position of the point on the surface.
- Screen space interpolation is used to compute $(u, v)$ at each pixel.
$$f_x = (1 - \alpha) \frac{x_0} {w_0} + \alpha \frac{x_1} {w_1}$$
- Perspective correct interpolation of $(u, v)$ is given by

$$f_x = \frac{(1 - \beta) x_0 + \beta x_1} {(1 - \beta) w_0 + \beta w_1}$$

- Post Perspective, use 
$$ \beta = \frac{\alpha * w_0}{(1 - \alpha) w_1 + \alpha w_0}$$

## Texture coordinates

How to specify mapping from an object to a texture? It should have the following properties

- ==Piecewise Linearity==: in order to use interpolation hardware
- ==Invertible==: go back and forth between object and texture space
- ==Easy to Compute==
- ==Area Preserving== or ==Angle Preserving==

Some Common texture mappings are 
- Linear/Planar/Hyperplanar Projection
- Cylindrical 
- Spherical
- Piecewise-linear or Piecewise-Bilinear on a plane from explicit per-vertex texture coordinates
- Normal-vector projection onto a sphere


!!! note
    Look at slides for images

| Texture Mapping | Description | Use case |
| --- | --- | --- |
| Planar Texturing | Image is projected orthographically onto the object. | Texturing flat surfaces |
| Cylindrical Texturing | Image is projected onto the object using a cylinder. | Texturing cylinders, cones, and other objects that have some central axis |
| Spherical Texturing | Image is projected onto the object using a sphere. | Texturing blobs, spheres, and other objects that are roughly spherical |
| Box Texturing | Image is projected onto the object from all six sides of a cube. | Texturing cubes and other objects that are roughly box-shaped |
| UV Texturing | Explicit per-vertex texture coordinates are used to map the texture onto the object. | Texturing objects with complex geometry |


## Texture filtering

- During texture mapping, one pixel on a textured surface may not correspond to one texel.
- Insufficient resolution may lead to aliasing artifacts/jaggies.
- Can lead to both minification and magnification artifacts.

| Method | Description |
| --- | --- |
| Nearest Neighbor | Simplest method, picks the nearest texel. |
| Bilinear | Find closest matching source pixel grid and interpolate between 4 neighboring texels. |
| Mipmapping | Precompute multiple versions of the texture at different resolutions using high-quality filtering, and then do nearest neighbor or bilinear filtering on the mipmap. |
| Anisotropic | Recognize when a texture is being stretched in one direction more than another and takes larger number of samples to compensate. |