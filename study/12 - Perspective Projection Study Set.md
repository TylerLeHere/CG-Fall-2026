# Lecture 12 · Perspective Projection

[Lecture PDF](<../slides/12 - Perspective Projection.pdf>) · [PowerPoint study guide](<12 - Perspective Projection Study Guide.pptx>) · [Final exam format](<Final exam format.md>)

Use the lecture’s camera convention throughout. The eye is at the origin and looks down negative $z$, so the near and far plane coordinates satisfy $f<n<0$. Write your answers first, then compare with the worked key.

## Recall

| Prompt | Slide pages |
| --- | --- |
| Why does moving an object twice as far away halve its projected height? | 4–7 |
| What does the last coordinate $w$ do? What happens if $w=0$? | 8–11 |
| What does $P$ do to the frustum, and what does $M_{\mathrm{orth}}$ do afterward? | 15–21 |
| How do vertical field of view and aspect ratio determine the near-plane rectangle? | 22–24 |

## Practice

1. **Light derivation · Similar triangles.** The image plane is at $d=-2$, and the top of an object is at $y=3$, $z=-6$. Use $y_s/d=y/z$ to find its projected height above the optical axis. What is the height after the object moves to $z=-12$?
2. **Explain differences · Orthographic and perspective.** Compare the view volume, apparent object size with distance, and what happens to parallel lines. Use train tracks as your example.
3. **Light derivation · Recover the depth row.** After division by $w=z$, assume $z'=(Az+B)/z$. Use $z'(n)=n$ and $z'(f)=f$ to find $A$ and $B$.
4. **Light derivation · Apply the projection.** Let $n=-2$ and $f=-10$. For a camera-space point $(3,1,-6)$, use $P(x,y,z,1)^T=(nx,ny,(n+f)z-fn,z)^T$. Find the homogeneous output and its Cartesian form. Explain why the depth coordinate differs from the original.
5. **Light derivation · Set up the frustum.** Let $n=-2$, vertical FOV $90^\circ$, and image size $1920\times1080$. Use $t=|n|\tan(\theta/2)$, $r=tW/H$, $b=-t$, and $l=-r$. Find $l,r,b,t$.
6. **Describe an algorithm · Object space to viewport.** Given an object-space vertex and the model, camera, projection, and viewport transforms, describe the operations in order. Explain where the perspective divide happens conceptually and why the renderer keeps depth.
7. **Light derivation · Nonlinear depth.** With $n=-1$, $f=-9$, compute $z'=n+f-fn/z$ for $z=-1,-2,-8,-9$. Which one-unit interval produces a larger change in $z'$?

## Worked answers

1. $y_s=dy/z=(-2)(3)/(-6)=1$. At $z=-12$, $y_s=0.5$. The eye, image point, and 3D point lie on one ray, giving similar triangles. Check that both heights are positive with this convention.
2. Orthographic maps a box and scales each projected dimension independently of depth. Parallel lines stay parallel. Perspective maps a frustum and scales $x,y$ by $n/z$. Parallel rails running into the distance approach a common vanishing point. Lines parallel to the image plane can remain parallel under perspective.
3. Substituting the near and far plane values gives $An+B=n^2$ and $Af+B=f^2$. Subtract to get $A(n-f)=(n-f)(n+f)$, so $A=n+f$. Then $B=n^2-(n+f)n=-fn$. Substitution checks both planes.
4. $Pp=(-6,-2,(-12)(-6)-20,-6)=(-6,-2,52,-6)$. Dividing by $-6$ gives $(1,1/3,-26/3)$. Perspective scales $x,y$ by $1/3$. The depth mapping has a $1/z$ term and fixes both endpoint planes.
5. $t=2\tan45^\circ=2$, $b=-2$, $r=2(16/9)=32/9$, and $l=-32/9$. The near-plane width-to-height ratio is $(64/9)/4=16/9$.
6. Apply the model transform to get world space and the camera transform to get camera space. Apply $P$ to encode $z$ in $w$, then $M_{\mathrm{orth}}$ to reach homogeneous clip coordinates for the canonical volume. A rasterizer clips in homogeneous space, divides surviving coordinates by $w$, and maps normalized coordinates to viewport coordinates. The course can group the affine viewport transform into the matrix product before the final divide for a point already known to be visible. Depth lets the depth test decide which overlapping fragment is closer under the chosen convention.
7. In order the results are $-1,-5.5,-8.875,-9$. The near interval changes by $4.5$, and the far interval changes by $0.125$. Both intervals have camera-space length 1. The reciprocal-depth term explains the different spacing.

### Recall key

Distance appears in the denominator of $y_s=dy/z$. Homogeneous representatives differ by a nonzero scale, and $w=0$ gives no finite Cartesian point after division. $P$ maps the frustum to a box after homogenization. $M_{\mathrm{orth}}$ maps that box to the canonical cube. Half the vertical field of view sets the near half-height, and the image aspect ratio sets the near half-width.
