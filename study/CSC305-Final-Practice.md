# CSC 305 final practice

Use this with the [study plan](CSC305-Final-Study-Plan.md) and the [combined guide](CSC305-Final-Study-Guide.pptx). The questions are original practice based on the course material. Keep the equations provided in each prompt visible. Cover the worked answers and respond in a few sentences, in labelled steps, or with a labelled sketch and a sentence explaining it.

For the 12 topic drills, try two at a time. For the six-question mock, try 35–45 minutes as a study target. That timing and the scoring below are for practice.

## Twelve topic drills

### 1 · Vector reasoning · Lectures 02 and 08

A triangle has vertices A = (0,0,0), B = (2,0,0), and C = (0,3,0). Given `n_raw = (B − A) × (C − A)` and `a × b = (a_y b_z − a_z b_y, a_z b_x − a_x b_z, a_x b_y − a_y b_x)`, find its raw normal. A raw normal `v` becomes unit length after dividing by `‖v‖ = √(v_x² + v_y² + v_z²)`. Give the unit normal and explain what changes if the face order swaps B and C. Sketch the plane and the two normal directions.

### 2 · Compare techniques · Lectures 01 and 04

A small red element with alpha 0.5 lies over a blue opaque background. Explain what alpha controls and why blending should use linear-light values. Given `C = αF + (1 − α)B` for an opaque background, compute the linear RGB when F = (1,0,0) and B = (0,0,1). State why the result has full opacity.

### 3 · Explain an algorithm · Lecture 05, Assignments 2 and 4

Two objects return forward intersections along the same primary ray. A sphere returns t = 1.5. The supporting plane of a triangle returns t = 0.5 with u = 0.8 and v = 0.4. The triangle’s weights are `(1 − u − v, u, v)`, and valid weights are nonnegative. Explain how a ray tracer selects the visible object. What changes if v is 0.1 instead?

### 4 · Compare techniques with a sketch · Lecture 05, Assignment 3

Sketch a point P on a reflective floor, a surface normal, an incoming camera ray, a reflected ray, a lamp and a shadow ray. Explain what question the shadow ray answers and what result the reflected ray contributes. Why do the two searches use different stopping conditions?

### 5 · Reason from a supplied equation · Lecture 06, Assignment 3

The two values to blend are a = 0.2 and b = 0.8. Given `blend(a,b,t) = (1 − t)a + tb` and the cubic fade `s(w) = 3w² − 2w³`, compute the linear and cubic blends at w = 0.25. Explain what smooth weighting changes across cell boundaries and why both rules agree at w = 0 and w = 1.

### 6 · Read a mesh and explain a trade-off · Meshes and Lecture 07, Assignment 4

An index buffer has faces (0,1,2) and (2,1,3). Identify the shared edge and show how it is traversed in each face. Compare an indexed face set with a halfedge representation for repeatedly finding a face’s neighbors. Draw the two triangles if that helps.

### 7 · Explain with a sketch · Lectures 09 and 12

Draw two equal-height objects at different positive distances from a camera. In perspective, given `h_image = d × h_object / z` where d is the positive image-plane distance and z is positive object distance, what happens to projected height when z doubles? How would an orthographic camera render the two heights at a fixed scale? State which rays are parallel.

### 8 · Explain an algorithm · Lectures 10 and 11, Assignment 5

For opaque triangles P and Q, fragments at one pixel have depths 0.6 and 0.2. Smaller depths are nearer. Describe how a rasterizer decides which fragments even reach the depth test and which colour is stored. Trace both draw orders.

### 9 · Compare techniques · Lectures 05 and 11, Assignment 5

On a low-resolution sphere mesh, flat shading shows clear facets. Vertex shading looks smoother but a narrow highlight vanishes. Explain both results using where normals come from, where lighting is evaluated, and what gets interpolated. Describe one change that could recover the highlight.

### 10 · Reason from supplied equations · Lecture 13

A screen sample lies halfway along an edge. The endpoints carry scalar texture coordinates a₀ = 0 and a₁ = 1, and clip coordinates w₀ = 1 and w₁ = 4. With screen weights λ₀ = λ₁ = 0.5, use `a = (Σ λᵢaᵢ/wᵢ)/(Σ λᵢ/wᵢ)` to compute the coordinate. Compare it with the direct screen-space average, and state when the two methods agree for all edge samples.

### 11 · Compare techniques · Lectures 13 and 14

A checkerboard texture looks stretched in one part of a mesh even in a close-up. In another part it shimmers only in the distance. Explain how each symptom could arise. Explain which operation would address each one and why.

### 12 · Explain an algorithm · Lecture 14

Describe how to put UV coordinates on a triangulated disk using uniform harmonic weights. Start from the boundary and explain what each interior equation means. Give two distinct checks for the result and one reason a seam might still be needed on a closed model.

## Six-question mixed mock

### M1 · Explain an algorithm · BVH and closest hit

A root box intersects a ray. Its two child boxes have entry parameters t = 1 and t = 3. The nearer child’s leaf triangle hits at t = 4. The other leaf triangle hits at t = 3.5. Explain how to find the correct hit and when you could safely prune a box. Sketch the four parameters on a ray. Assume all values use the same forward ray and both leaf hits are valid.

### M2 · Compare techniques · Surface visibility and texture sampling

A rasterized scene has jagged edges on a blank rooftop and moving moiré bands on a distant textured floor. Explain which problem is about coverage and which is about texture frequency. Compare supersampling and mipmapping on what each averages, and say which technique you would try for each symptom.

### M3 · Apply a supplied formula and sketch · Camera geometry

A camera has vertical FOV θ = 90°, positive near distance d = 3, and image aspect A = W/H = 4/3. Given `h = d tan(θ/2)`, `w = Ah`, and `tan 45° = 1`, compute the half-height and half-width of the near rectangle. Draw a side view and mark why θ/2 enters. If only the framebuffer width doubles, what changes?

### M4 · Explain a geometric decision · Signed fields

In a marching-squares cell, two corners on one edge have field values −2 and +6. Let endpoint positions be A = (1,1), B = (5,1). Using `F(t) = (1 − t)F(A) + tF(B)` and `p(t) = (1 − t)A + tB`, find the crossing. Then explain why sampling signs at grid corners can miss a small feature entirely inside one cell.

### M5 · Compare and check · UV validity

A chart’s triangles have expected winding and positive UV area, but two distant faces land on the same UV region. Another chart is one-to-one and has no flipped triangles, but its checker cells look skewed. Explain what each chart passes and fails. How could cutting another seam affect distortion and continuity?

### M6 · Apply a supplied formula · Surface orientation

For a triangle edge with tangent `t = (1,1)` and normal `n = (−1,1)`, scale x by 2 and y by 1 with `S = diag(2,1)`. You are given `S⁻ᵀ = diag(1/2,1)`. For each candidate normal `Sn` and `S⁻ᵀn`, compute its dot product with `St`, using `a·b = aₓbₓ + aᵧbᵧ`. Which rule preserves perpendicularity? Why normalize the selected normal before using it for lighting?

## Worked answers

### Topic drills

| Question | Model answer and check |
| --- | --- |
| 1 | B − A = (2,0,0) and C − A = (0,3,0). The raw normal is (0,0,6), so the unit normal is (0,0,1). Swapping the two edges reverses the normal to (0,0,−1). In a sketch the triangle lies in the xy plane, with the two normals along opposite z directions. |
| 2 | Alpha 0.5 gives half the source colour and leaves half of the background contribution visible. In linear light the result is 0.5(1,0,0) + 0.5(0,0,1) = (0.5,0,0.5). The blue background already covers every part of the sample, so the composite is fully opaque. Decode nonlinear RGB before averaging light. |
| 3 | The first triangle weights are (−0.2,0.8,0.4). The plane hit lies outside the triangle, so the sphere at 1.5 wins. With v = 0.1 the weights are (0.1,0.8,0.1). The triangle is now valid and t = 0.5 wins. The weights sum to 1 in both cases. |
| 4 | Draw the normal at P, the incoming camera ray ending at P, its mirror direction departing P at the same angle to the normal line, and a ray from P to the lamp. The shadow ray only asks if an object blocks the segment before the lamp. The reflection ray seeks the nearest valid scene hit in its reflected direction, then returns its shaded colour subject to the bounce budget. |
| 5 | Linear gives 0.75(0.2) + 0.25(0.8) = 0.35. The cubic weight is 3(1/16) − 2(1/64) = 0.15625. Blending gives 0.2 + 0.6(0.15625) = 0.29375. The cubic weight eases in and out with zero endpoint slope, softening boundary transitions. Both weights equal the endpoint values 0 and 1 there. |
| 6 | The shared edge is 1–2. The first face traverses 1 → 2 and the second traverses 2 → 1, which is consistent for adjacent faces. An indexed face set stores shared positions compactly. Finding neighbors requires connectivity lookup or additional indexing. Halfedges add directed connectivity, such as a twin across the edge, for efficient traversal at the cost of extra storage. |
| 7 | With fixed d and object height, doubling z halves the projected height. Label the common eye, image plane and the two object distances in the perspective sketch. In orthographic projection, equal-height objects at a fixed scale project to equal heights because the rays are parallel. Perspective rays from a single eye fan out. |
| 8 | Project and clip triangles, then test whether each triangle covers the pixel sample. Candidate fragments carry interpolated attributes and depth. If P arrives first, 0.6 is stored then Q replaces it with 0.2. If Q arrives first, 0.2 is stored and P fails the depth test. Q’s colour wins in both orders. |
| 9 | Flat shading uses the same face normal at the corners of each face. Adjacent faces can have different normals. Vertex shading uses averaged normals at vertices and blends the lit colours, which smooths transitions. If none of those vertices samples the bright spot, their colours contain no peak to interpolate. Interpolate normals and evaluate lighting per fragment, or add more geometry samples. |
| 10 | The numerator is 0.5(0)/1 + 0.5(1)/4 = 0.125. The denominator is 0.5/1 + 0.5/4 = 0.625. Thus a = 0.2, while the direct screen average is 0.5. Equal endpoint w values cancel from the ratio. A constant attribute also agrees under either method. |
| 11 | Stretch visible up close suggests the UV chart changes shape or texel density. Inspect the chart with a checkerboard and adjust UV placement or seams. Distance-dependent shimmer suggests too many texels per screen pixel, so prefilter with mipmaps or a filter suited to the footprint. A different chart cannot replace frequency filtering. |
| 12 | Order the disk boundary and place it around a convex polygon in the same order. Give edges weight 1. Each interior UV must equal the average of its neighbors. Solve the coupled equations, treating boundary UVs as known. Check signed face orientation and nonlocal overlap separately. A closed surface needs a cut or multiple charts for a planar layout. |

### Mixed mock

| Question | Model answer and check |
| --- | --- |
| M1 | Test the root, then visit boxes the ray hits. The closer box gives a triangle hit at 4, so record 4. The second box starts at 3, before 4, so it could contain a closer triangle. It does, at 3.5. The ray sketch has markers in the order 1, 3, 3.5, 4. Prune a box when the ray misses it or its earliest reachable parameter is beyond the current closest hit. |
| M2 | The roof edge crosses pixels that a single point sample treats as fully covered or empty. Supersampling averages several subpixel results and makes coverage transitions smoother. The distant floor puts many texels inside a pixel footprint. A mip level stores filtered texel values that approximate that footprint and reduce bands or shimmer. Supersampling can also reduce texture aliasing if enough subpixel texture samples are taken. |
| M3 | h = 3 tan 45° = 3. w = (4/3) × 3 = 4. Draw the eye on a horizontal centre line and a vertical near plane 3 units away. The right triangle uses the top edge and the centre line, half the angle between top and bottom rays. Double only the width and the aspect doubles. The half-width becomes 8 and the half-height stays 3. |
| M4 | Set 0 = (1 − t)(−2) + 6t = −2 + 8t, so t = 1/4. Hence p = 0.75(1,1) + 0.25(5,1) = (2,1). The crossing correctly lies closer to the endpoint with smaller absolute field value. All corners can have the same sign even when a tiny enclosed region between them has the opposite sign. |
| M5 | The first chart’s per-face orientation passes, but the overlap means distinct surface locations share a UV. The second chart passes those validity checks, while its skew reveals angle distortion. Splitting a chart can give both pieces more room to flatten, at the cost of more seams to paint, align or pad in the texture. |
| M6 | St = (2,1). Sn = (−2,1), giving (−2)(2) + 1(1) = −3. S⁻ᵀn = (−0.5,1), giving (−0.5)(2) + 1(1) = 0. Use the inverse transpose for normals. Normalize so a dot product with another unit direction represents the cosine of the angle. |

## Mark your reasoning

For each answer, award one practice point for the **result**, one for the **reason**, and one for a **check or useful label**. Record the first error in each answer. If you chose the wrong rule, explain the rule with one edge case. If you chose the right rule and lost the sign, redo the arithmetic. If your answer was correct but hard to follow, rewrite it in three short steps. The point total is a way to track your review.
