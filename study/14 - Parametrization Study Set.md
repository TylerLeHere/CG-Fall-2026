# Lecture 14 · Mesh Parametrization

[Lecture PDF](<../slides/14 - Parametrization.pdf>) · [PowerPoint study guide](<14 - Parametrization Study Guide.pptx>) · [Final exam format](<Final exam format.md>)

Lecture 13 uses UV coordinates to look up texture values. Lecture 14 explains how to assign those coordinates to a mesh in the first place.

## Recall

| Prompt | Slide pages |
| --- | --- |
| Which way does $P$ map? What does flattening do? | 3–4 |
| How do area and angle distortion show up in a checkerboard? | 5–8 |
| What distinguishes a folded triangle from overlap between distant triangles? | 9–11 |
| Why do seams help, and what does a seam cost? | 12–20 |
| Why is every free UV an average of its neighbours in a uniform harmonic map? | 21–33 |
| Which boundary and weight conditions support a fold-free, one-to-one map? | 34–38 |

## Practice

1. **Light derivation · Map a point between triangles.** A 3D triangle has vertices $A=(0,0,1), B=(4,0,1), C=(0,2,1)$. Its UV triangle has $a=(0,0), b=(0.5,0), c=(0,1)$. Use the weights $(\alpha,\beta,\gamma)=(0.25,0.5,0.25)$ and the interpolation rule $p=\alpha A+\beta B+\gamma C$, applied to the corresponding corners in each domain. Find the corresponding point in both domains and explain why you can reuse the weights.
2. **Explain differences · Area and angle distortion.** A planar chart applies either $U(x,y)=(2x,2y)$ or $V(x,y)=(2x,y/2)$. Describe the area and shape change in each case. Use the unit square to check area. For the diagonal use $\tan\theta=\text{height}/\text{width}$ and $\arctan(0.25)\approx14^\circ$. Which chart keeps a square checker pattern square?
3. **Light derivation · Diagnose a flipped face.** For consistently oriented mesh faces, oriented double area in UV space is $\det(b-a,c-a)$. Let $a=(0,0), b=(1,0), c=(0,1)$. Compute the sign for $(a,b,c)$ and for $(a,c,b)$. If all faces have positive area, can you conclude that every pair of UV triangle interiors is disjoint?
4. **Explain differences · Cut versus segment.** Compare a single long seam with several chart boundaries when flattening a sphere. Explain the trade-off in distortion, texture continuity, and what needs to be checked after placing the charts in an atlas.
5. **Describe an algorithm · Compute a harmonic UV map.** Given a triangulated mesh patch that is topologically a disk, explain how to produce a UV for each vertex. State the boundary conditions, the edge weight choice, how the linear system is assembled, and how to check the result.
6. **Light derivation · Equilibrium of one free vertex.** Let $E_i=\tfrac12\sum_jk_{ij}\|u_i-u_j\|^2$ with neighbours fixed at $(0,0),(2,0),(0,2)$ and weights $1,3,2$. Use $\nabla_{u_i}E_i=\sum_jk_{ij}(u_i-u_j)$ and set it to zero. Solve for $u_i$, then check the result lies inside the neighbours’ triangle.
7. **Light derivation · Assemble a two-vertex system.** Interior vertices $p,q$ are neighbours. Vertex $p$ is also adjacent to boundary points $A=(0,0), B=(2,0)$. Vertex $q$ is adjacent to $C=(2,2), D=(0,2)$. All listed weights are 1. Use $(\sum_j k_{ij})u_i-\sum_{j\ \mathrm{interior}}k_{ij}u_j=\sum_{j\ \mathrm{boundary}}k_{ij}u_j$. Write the two rows and solve both UV vectors.
8. **Explain differences · Uniform and cotangent weights.** Compare the two choices on what information goes into the weights, expected distortion and conditions for bijectivity. Use the edge formula $k_{ij}=\cot\alpha+\cot\beta$ and the opposite angles $120^\circ$ and $80^\circ$ as a concrete example. Given $\cot120^\circ\approx-0.577$ and $\cot80^\circ\approx0.176$, what would you infer about the guarantee?

## Worked answers

1. In 3D, $0.25A+0.5B+0.25C=(2,0.5,1)$. In UV, $0.25a+0.5b+0.25c=(0.25,0.25)$. The map inside a triangle is affine, so barycentric weights identify the same relative position in both domains. These weights sum to 1.
2. Under $U$, the square becomes $2\times2$ so area grows by a factor of 4. Its diagonal still makes a $45^\circ$ angle with the bottom edge. Under $V$, it becomes $2\times0.5$, so area stays 1 while the diagonal angle becomes $\arctan(0.25)\approx14^\circ$. $U$ preserves the square shape. $V$ preserves area and changes the shape.
3. $\det((1,0),(0,1))=1$. Swapping the last two positions changes the sign to $-1$. A negative value relative to the expected winding signals a flip. A zero value signals collapse. Positive signs check each face’s orientation. Distant triangles can still overlap, so inspect the boundary or check for global intersection as well.
4. A single slit can open the sphere into one disk-like chart and limit the amount of seam to manage. Flattening the whole surface in one chart can concentrate distortion. Multiple patches have more freedom to flatten with less distortion. They introduce more boundaries where patterns may break or filtering may show a seam. Place the islands without overlap and leave padding around them for filtering.
5. Start with mesh vertices, faces and an ordered boundary loop. If needed, cut the mesh into disk-like patches first. Fix the boundary vertices in order around a convex polygon. Choose edge weights and add one equilibrium row per free vertex. Keep unknown interior terms on the left and move known boundary terms to the right. Solve the sparse system for the two UV components. Return the UVs with the original face correspondence, checking triangle orientation, overlap and distortion.
6. Differentiate to get $\sum_jk_{ij}(u_i-u_j)=0$. Thus $u_i=(1(0,0)+3(2,0)+2(0,2))/(1+3+2)=(1,2/3)$. For this triangle, $x\ge0$, $y\ge0$ and $x+y\le2$. Here $x+y=5/3$. Each normalized weight is positive.
7. The rows are $3p-q=A+B=(2,0)$ and $-p+3q=C+D=(2,4)$. From $q=3p-(2,0)$, substitution gives $8p=(8,4)$. So $p=(1,0.5)$ and $q=(1,1.5)$. Verify $p=(q+A+B)/3$ and $q=(p+C+D)/3$.
8. Uniform weights use mesh connectivity, giving each neighbour equal pull. On a disk mesh with the boundary fixed in order on a convex polygon, uniform weights meet the lecture’s sufficient conditions for a bijective map. Cotangent weights also use the 3D triangle angles and often reduce local distortion, but here the edge weight is about $-0.401$. The sufficient condition fails. A negative weight means the guarantee no longer applies, while the actual UV output still needs checking.

### Recall key

$P$ maps the flat domain to the surface. Flattening applies the inverse when the map is one-to-one. A checkerboard changes size under area distortion and changes shape under angle distortion. Local fold and global overlap checks catch different failure modes. Harmonic mapping balances weighted neighbours with a fixed boundary. A convex boundary and appropriate nonnegative weights under the lecture’s disk-mesh assumptions provide the bijectivity guarantee. A fixed boundary can still cause distortion.
