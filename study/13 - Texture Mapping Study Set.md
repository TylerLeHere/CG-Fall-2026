# Lecture 13 · Texture Mapping

[Lecture PDF](<../slides/13 - Texture Mapping.pdf>) · [PowerPoint study guide](<13 - Texture Mapping Study Guide.pptx>) · [Final exam format](<Final exam format.md>)

Think of texture mapping as two steps. First find the fragment’s UV coordinate on the triangle. Then filter the texture image at that UV.

## Recall

| Prompt | Slide pages |
| --- | --- |
| Which surface property does each kind of map store or affect? | 4–15 |
| Why can one mesh position have multiple UVs? What can a checkerboard reveal? | 16–24 |
| Where do nearest and bilinear sampling each get their texel values? | 25–34 |
| Why can a seam show up even when its UV indices are correct? | 35 |
| What determines the apparent frequency of a sampled stripe and the mip level used? | 36–42 |

## Practice

1. **Explain differences · Choose the map.** For a brick wall, compare a colour texture, a normal map, and displacement. Explain which can show a jagged outline and why. Compare on geometry and shading.
2. **Describe an algorithm · Shade a fragment.** Given a triangle with positions and UVs, a texture and a camera, describe the path to a textured fragment. Explain why interpolating UVs can show details inside a large triangle. If you discuss perspective correction from screen-space weights $\lambda_i$, use $q=(\sum_i\lambda_iq_i/w_i)/(\sum_i\lambda_i/w_i)$, where $q_i$ are vertex UVs and $w_i$ are the homogeneous clip coordinates.
3. **Describe an algorithm · Encode a seam.** Two geometry faces are $(A,B,C)$ and $(A,C,D)$. Their UV tuples are $(1,2,3)$ and $(6,4,5)$. Build the unique $(\text{position},\text{UV})$ pairs for one draw index buffer. Which normals should duplicated vertices receive if the surface is meant to stay smooth?
4. **Light derivation · Bilinear filter.** Let $A=12,B=28,D=44,C=60$, with $A,B$ on the bottom row and $D,C$ on top. The local offsets are $u=0.75$, $v=0.25$. Use $E=(1-u)A+uB$, $F=(1-u)D+uC$, $G=(1-v)E+vF$. Find $G$ and the nearest texel.
5. **Explain differences · Magnification, minification and seams.** A checkerboard floor is viewed at a shallow angle. Describe what happens near the camera and near the horizon, and choose a filter for each. Separately, explain why a red UV island next to blue padding in an atlas can develop a blue edge.
6. **Light derivation · Aliased stripes.** At one sample per pixel, use $f_{\mathrm{seen}}=|f-\operatorname{round}(f)|$ and $f_N=f_s/2$. Find the alias of a cosine stripe at $f=0.8$ cycles/pixel, then show why the original and alias agree at each integer pixel $n$.
7. **Light derivation · Mipmap selection.** A $512\times512$ texture covers about $64\times64$ pixels. Assume a roughly square footprint and halve each dimension per level. Which mip level should be sampled? How many levels are there through $1\times1$? Estimate the total storage relative to the base level using $1+r+r^2+\ldots\approx1/(1-r)$ for a sufficiently long series with $0<r<1$.

## Worked answers

1. A colour map provides material colour, such as red brick versus gray mortar. A normal map provides directions for lighting, such as simulated grooves, while leaving the mesh positions as they are. Displacement moves the surface by a stored offset, often along the geometric normal, so a sufficiently resolved mesh can show the grooves and chips in silhouette.
2. Transform positions and pass along each UV. Rasterize the triangle to find the covered samples and their interpolation weights. Compute the UV, filter the image at that UV, and use the result in fragment shading. A fragment can fetch any nearby texels even on a large triangle. If $\lambda_i$ are screen-space weights and $w_i$ the clip-space homogeneous coordinates, use $q=(\sum_i\lambda_iq_i/w_i)/(\sum_i\lambda_i/w_i)$ for UV $q$. This reduces to ordinary interpolation when all $w_i$ are equal.
3. The pairs are $(A,1),(B,2),(C,3),(A,6),(C,4),(D,5)$. With these stored in order, the index tuples are $(0,1,2)$ and $(3,4,5)$. $A$ and $C$ each split into two GPU vertex records. Compute the smooth normals on the original connected mesh, then copy the original normal to all UV duplicates of a position.
4. $E=0.25(12)+0.75(28)=24$. $F=0.25(44)+0.75(60)=56$. $G=0.75(24)+0.25(56)=32$. Nearest chooses the bottom-right texel $B=28$. A useful check is $24\le G\le56$.
5. Nearby, one texel can cover many pixels. Bilinear filtering smooths the block boundaries seen with nearest. Far away, one pixel can cover many texels. A lower-resolution prefiltered mip level approximates their average and reduces moiré. Near a chart edge, bilinear or mip filtering can include values from the padding. Extend the island’s edge colours into a gutter and leave enough room for filtering at the chosen mip levels.
6. $f_N=0.5$ cycles/pixel and the alias is $|0.8-1|=0.2$ cycles/pixel. At integer $n$, $2\pi(0.8)n=2\pi n-2\pi(0.2)n$. Periodicity removes $2\pi n$, then cosine symmetry removes the minus sign. The samples alone cannot distinguish the stripes.
7. There are $512/64=8=2^3$ base texels across one pixel, so use level 3. Levels 0 through 9 run from 512 to 1, for 10 levels total. Each level uses one quarter of the previous level’s texel count, so total storage is just below $4/3$ of base storage, assuming the same bytes per texel and no overhead.

### Recall key

A checkerboard can expose stretching, compression, and skew. A seam splits UV coordinates even when a 3D edge is shared. Nearest picks one texel. Bilinear blends four in two horizontal blends followed by a vertical blend. The vertical blend uses $v$ for the top row weight. Slide 31 prints $u$ there, and the endpoint check $v=1\Rightarrow G=F$ shows why $v$ is needed.
