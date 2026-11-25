# CSC 305 final study plan

Start with one question. **How does a 3D scene become a grid of coloured pixels?** The ray tracer starts at a pixel and searches the scene for a surface. The rasterizer starts at a triangle and finds the pixels it covers. Both need the same ideas about coordinates, visibility, materials, and light.

Use the [combined PowerPoint](CSC305-Final-Study-Guide.pptx) to learn a concept, then work through [CSC305-Final-Practice.md](CSC305-Final-Practice.md) with the answer key covered. The lecture and assignment links below lead to specific source pages or exercises whenever you need to fix a misunderstanding.

## What the final asks you to do

The instructor’s update says the final is **primarily short answer** and tests concepts, algorithms, comparisons, and mathematical or geometric reasoning. **Nontrivial equations needed for a question will be supplied.** Use lectures and recordings for the underlying ideas. Use assignments to explain what an algorithm is doing and why. [Final exam format](<Final exam format.md>) · [Lecture 07, p. 2](<../slides/07 - Spatial Data Structures.pdf>)

| If you are asked to… | Aim for |
| --- | --- |
| Describe an algorithm | State the inputs and outputs. Give the essential steps in order and explain why the key condition is valid. |
| Compare techniques | Compare them on the same property. Give a small example that shows why the difference matters. |
| Apply a given formula | Define the symbols and convention, substitute or rearrange, and interpret the result. Check a sign, range, endpoint, or limiting case. |
| Explain geometry with a sketch | Label the eye, ray, normal, axes, boundary or other relevant features. Refer to the labels in the explanation. |

**Before November 30.** Complete the six blocks in the compressed plan if time allows, or use the 12-session route if you have more room. Take two questions to the review lecture. Mark the exact decision you find hard to explain, such as why a box hit is insufficient or where perspective division happens.

**At the November 30 review.** Write down the instructor’s prompt wording, the formulas or diagrams supplied, and which steps the instructor included in a complete answer. Do the example yourself before copying the explanation when there is time.

**After the review.** Redo the instructor’s examples unaided, adjust your answer length using those examples, then try the unseen mock in the practice sheet. Repair the weakest topics with the original PDFs or the previous offering’s recordings under **Brightspace → Content**.

## How to use each session

Budget **75–100 minutes**. The week is flexible around your other courses and exam schedule.

1. **Recall for about 10 minutes.** Close the notes and sketch or explain one idea from the previous session.
2. **Learn for 25–30 minutes.** Read the assigned original slides. If you lose the thread, open the corresponding Brightspace recording and pause before the instructor reveals the next step.
3. **Trace for 20 minutes.** Follow one example from an assignment on paper. Identify what goes in, what rule makes the decision, and what comes out.
4. **Write for 15–25 minutes.** Answer two short prompts. Where a formula is supplied, leave the question and formula visible and work out the rest unaided.
5. **Check for 5–10 minutes.** Mark the first missing step. Redo it the next day and again three sessions later.

## 12-session schedule

| Session | Concepts and source pages | Assignment or by-hand trace | Ready to move on when you can… |
| --- | --- | --- | --- |
| 1 · Vectors and geometric tests | L02 pp. 4–28, 30–41. L03 pp. 9–12, 16–25, 27–47. Points and vectors, dot and cross products, matrices and systems. Skim C++ context if it helps you follow mesh data, references or the assignment workflow. | **A1, optional.** Read a tiny XYZ sample or sketch an indexed OBJ polygon. Cast a segment from an inside point and an outside point. Count crossings and explain the shared-vertex case. | Compute a displacement and a triangle normal, then explain why odd crossings mean inside. |
| 2 · Images and rendering | L01 pp. 15–17. L04 pp. 6–13. Pixels, framebuffers, RGB, gamma and alpha. | Compare A2’s image output with A5’s framebuffer. Blend half-opaque red over opaque blue using linear RGB. | Tell which direction the ray and triangle workflows go, and explain the linear-light assumption behind the blend. |
| 3 · Rays, intersections and lighting | L05 pp. 3–15, 16–47, 49–67. Rays, projection, sphere roots, bounded planar primitives and local shading. | **A2.** Trace one primary ray until you pick its nearest valid hit. Compare a triangle with a parallelogram at u = 0.75, v = 0.75. Test diffuse light when n·l is negative. | Explain what each unknown means, why a hit needs a positive t, and where ambient, diffuse and specular colours come from. |
| 4 · Camera field of view and secondary rays | L05 pp. 68–72. L07 pp. 7–22. Ray Tracing II pp. 10–24, 29–44, 60–65. | **A3.** Draw the FOV right triangle, compare one blocker before the light with one beyond it, and hand-trace one reflection. Read depth of field and refraction as bonus extensions. | Derive the sensor half-size, distinguish primary, shadow and reflection rays, and explain what path tracing adds to direct local lighting. |
| 5 · Procedural textures and implicit surfaces | L06 pp. 3–29, 32–39, 47–54, 58–74, 78–106. | **A3 Perlin.** Pick four grid gradients, form the offsets and dot products, then blend horizontally and vertically. Separately use two signed endpoints to find a contour crossing. | Explain how a noise value differs from a texture lookup, and when a signed distance permits a safe ray step. |
| 6 · Meshes and acceleration | Extra Meshes pp. 2–31, 35–47. L07 pp. 23–46, 67–78, 101–113, 114–161. | **A4.** Decode a tiny OFF mesh. Draw a two-level AABB tree, merge child boxes, and walk a ray through its slabs. Compare the result with brute force. | Distinguish a primitive grouping from a space partition. Explain why a box miss permits pruning and a box hit still needs a triangle test. |
| 7 · Object motion, cameras and projection | L08 pp. 19–46, 52–74, 75–97. L09 pp. 3–10, 11–33, 34–52. L12 pp. 3–7, 11–24. | **A5 transformations.** Rotate one point about a nonzero pivot, map one world point into eye coordinates, and divide two clip-space points by w. Tie A3’s FOV to the projection frustum. | Name each coordinate space in order, explain the view transform as the inverse camera pose, and show why distant points shrink in perspective. |
| 8 · Rasterization theory | L10 pp. 5–26, 27–61, 62–79. L11 pp. 14–43. | **A5 pipeline.** Test a pixel centre against one triangle. Interpolate a colour, compare two fragment depths, and average a few coverage samples. | Explain coverage, clipping, interpolation, visibility, blending and antialiasing as distinct operations. |
| 9 · Rasterizer stages and shading | L11 pp. 45–63. L09 pp. 34–52. L12 pp. 17–24. | **A5 exercise chain.** Load the mesh, reproduce its silhouette, follow edge vertices through wireframe, compare normals, trace depth, then explain pivot animation and the perspective camera. Use assignment renders to explain what each stage changes. | Trace one vertex and one fragment on paper and explain what changes between uniform, wireframe, flat and per-vertex renders. |
| 10 · Texture mapping | L13 pp. 4–13, 15–24, 25–42. Revisit L06 interpolation and L12 perspective. | **Conceptual extension of A5.** Add UVs on paper to three vertices. Compute a fragment UV and bilinear texel colour. Compare magnification with minification and choose a mip level. | Distinguish UV interpolation from texel filtering, and colour maps from normal and displacement maps. |
| 11 · Mesh parametrization | L14 pp. 3–11, 12–20, 21–38. Revisit Meshes boundary and adjacency. | **Conceptual extension of A4 and A5.** Use the same weights in a 3D triangle and its UV triangle. Check a signed UV area, then solve a one- or two-vertex spring equilibrium. | Explain why cuts help, how to assemble a harmonic row, and what a negative cotangent weight means for the guarantee. |
| 12 · Mixed mock and repair | Use the separate six-question mock. Keep the prompt and supplied formulas visible, with notes and answers covered. | Try **35–45 minutes** as a study target. Spend 25 minutes marking your answers, then redraw or recompute the weakest example. | Produce one complete answer of each format with only the question and any supplied equations visible. Explain both rendering pipelines, including where the colour, visibility and UV data come from. |

## How the assignments fit together

| Assignment | What you actually follow through | Compare or check |
| --- | --- | --- |
| [A1 · Basic geometry and C++](../Assignment_1/README.md), optional | XYZ and OBJ inputs, segment intersection, bounding box, outside endpoint and even–odd count | One crossing for a simple inside point, two or zero for a simple outside point. Handle a ray through a polygon vertex consistently. |
| [A2 · First ray tracer](../Assignment_2/README.md) | Primary rays, sphere and parallelogram intersections, projection and RGB lighting | Nearest forward root, in-bounds planar parameters, and normal orientation. Orthographic rays are parallel. Perspective rays fan out. |
| [A3 · Ray effects](../Assignment_3/README.md) | Intersections, FOV, Phong-family shading, finite shadow rays, reflection and Perlin. Bonus depth of field and refraction. | Trace from the actual hit point, distinguish the light distance from infinity, and verify the bounce termination and interpolation endpoints. |
| [A4 · Mesh ray tracing](../Assignment_4/README.md) | Mesh faces, ray/triangle test, nearest hit, AABB slab test, centroid split, top-down BVH. Bonus primitives, shadows and reflections. | A BVH changes how many triangles you test. Check that the accelerated path returns the same closest valid hit as brute force. |
| [A5 · Software rasterizer](../Assignment_5/README.md) | Orthographic silhouette, wireframe, flat and per-vertex shading, depth, pivot rotation and GIFs, perspective camera | Follow positions and shading spaces separately. Verify aspect ratio, normal choice, fragment depth and rotation around the intended centre. |

Lectures 13 and 14 extend the pipeline conceptually. Texture sampling uses UVs during shading. Parametrization decides what UVs the mesh carries. The A5 specification ends with the perspective camera.

## Six-session compressed plan

Use this when you have six study blocks. Budget about two hours per block. To work toward the November 30 review, use the first five blocks for topic review and the sixth for a short mock and a list of questions. Save the separate mock for after the review if you have already tried the guide’s mock.

| Block | Combine | One trace to finish |
| --- | --- | --- |
| 1 | Sessions 1–2 and 3 | One A2 pixel from camera ray to shade. Review vector operations and pixels as they appear in that trace. |
| 2 | Sessions 4–5 | FOV triangle, blocker distance, one reflection vector, one Perlin blend. Review extra light transport and implicit surfaces from the deck. |
| 3 | Session 6 | A4 triangle hit and nearest-hit BVH traversal. Explain the difference between BVH, grid and k-d tree. |
| 4 | Sessions 7–8 | A5 triangle from object coordinates through clip and screen coordinates, including a coverage and depth decision. |
| 5 | Sessions 9–11 | One A5 lighting example, one texture sample, and one UV equilibrium row. Connect normals, texels and UV coordinates to the right stage. |
| 6 | Session 12 | Short algorithm, comparison and reasoning answers. Redo the first step you missed on each. |

## Lecture-by-lecture review

The page numbers in the schedule use PDF order. Find the lecture and its detailed guide below. Then use the checklist to decide whether you can explain the main idea on paper.

| Lecture | Original slides | Detailed guide |
| --- | --- | --- |
| 01 · Introduction | [Lecture 01 PDF](<../slides/01 - Introduction to Computer Graphics.pdf>) | [Introduction and Images](<01 and 04 - Introduction and Images Study Guide.pptx>) |
| 02 · Basic linear algebra | [Lecture 02 PDF](<../slides/02 - Basic Linear Algebra.pdf>) | [Linear Algebra](<02 - Basic Linear Algebra Study Guide.pptx>) |
| 03 · C++ | [Lecture 03 PDF](<../slides/03 - C++.pdf>) | [C++](<03 - C++ Study Guide.pptx>) |
| 04 · Images | [Lecture 04 PDF](<../slides/04 - Images.pdf>) | [Introduction and Images](<01 and 04 - Introduction and Images Study Guide.pptx>) |
| 05 · Ray tracing | [Lecture 05 PDF](<../slides/05 - Ray Tracing.pdf>) | [Ray Tracing](<05 - Ray Tracing Study Guide.pptx>) |
| 05 extra · Ray tracing II | [Ray Tracing II PDF](<../slides/05 - Ray Tracing II.pdf>) | Combined guide, session 4 |
| 06 · Procedural synthesis | [Lecture 06 PDF](<../slides/06 - Procedural Synthesis.pdf>) | [Procedural Synthesis](<06 - Procedural Synthesis Study Guide.pptx>) |
| 07 · Spatial data structures | [Lecture 07 PDF](<../slides/07 - Spatial Data Structures.pdf>) | [Spatial Data Structures](<07 - Spatial Data Structures Study Guide.pptx>) |
| 07 extra · Meshes | [Meshes PDF](<../slides/07 - Meshes.pdf>) | [Spatial Data Structures, mesh recap](<07 - Spatial Data Structures Study Guide.pptx>) |
| 08 · 2D transformations | [Lecture 08 PDF](<../slides/08 - 2D Transformations.pdf>) | [2D Transformations](<08 - 2D Transformations Study Guide.pptx>) |
| 09 · Viewing transformations | [Lecture 09 PDF](<../slides/09 - Viewing Transformations.pdf>) | [Viewing Transformations](<09 - Viewing Transformations Study Guide.pptx>) |
| 10 · Rasterization theory | [Lecture 10 PDF](<../slides/10 - Rasterization - Theory.pdf>) | [Rasterization Theory](<10 - Rasterization Theory Study Guide.pptx>) |
| 11 · Rasterization implementation | [Lecture 11 PDF](<../slides/11 - Rasterization - Implementation.pdf>) | [Rasterization Implementation](<11 - Rasterization Implementation Study Guide.pptx>) |
| 12 · Perspective projection | [Lecture 12 PDF](<../slides/12 - Perspective Projection.pdf>) | [Perspective Projection](<12 - Perspective Projection Study Guide.pptx>) · [Practice set](<12 - Perspective Projection Study Set.md>) |
| 13 · Texture mapping | [Lecture 13 PDF](<../slides/13 - Texture Mapping.pdf>) | [Texture Mapping](<13 - Texture Mapping Study Guide.pptx>) · [Practice set](<13 - Texture Mapping Study Set.md>) |
| 14 · Parametrization | [Lecture 14 PDF](<../slides/14 - Parametrization.pdf>) | [Parametrization](<14 - Parametrization Study Guide.pptx>) · [Practice set](<14 - Parametrization Study Set.md>) |

### One exam-style task per lecture

Use the practice key after you write your answer. The drill and mock numbers refer to [CSC305-Final-Practice.md](CSC305-Final-Practice.md). Keep supplied equations visible.

| Lecture | Ready when you can… | First practice to try |
| --- | --- | --- |
| 01 · Introduction | Compare the same opaque scene under ray tracing and rasterization. Explain what each starts with and how each finds the visible surface. | Combined guide, slide 88. |
| 02 · Basic linear algebra | Sketch two triangle edges and their normal. Use the supplied cross-product formula and explain how swapping the edge order affects the answer. | Final practice drill 1. |
| 03 · C++ | Use this as assignment context. Explain how an indexed list of positions and faces represents a mesh and what an intersection routine returns. | Meshes drill 6. The C++ deck's two language questions are optional background. |
| 04 · Images | Explain what alpha controls, why the blend uses linear-light values, and how to identify the pixel centre under the stated grid convention. | Final practice drill 2. |
| 05 · Ray tracing | Walk through a primary ray’s valid hits and choose the nearest one. Then sketch the shadow and reflection rays and explain why their stopping rules differ. | Final practice drills 3–4. |
| 05 extra · Ray tracing II | Explain how a white object near a red wall could acquire a reddish tint with indirect lighting. Compare what the two methods sample and why averaging helps. | Combined guide, slides 30–31. |
| 06 · Procedural synthesis | Explain one Perlin sample and sketch the zero crossing on an edge. Distinguish the sign of an implicit field from a safe distance step. | Final practice drill 5 and mock M4. |
| 07 · Spatial data structures | Sketch two BVH child boxes and mark their entry parameters. Explain why the first box hit cannot establish the closest surface. | Final practice mock M1. |
| 07 extra · Meshes | Draw two indexed faces. Name their common edge, trace its direction in each face, and explain what halfedges add for neighbor lookup. | Final practice drill 6. |
| 08 · 2D transformations | Explain how to rotate around a pivot. Then use a supplied matrix and dot product to test a normal after nonuniform scale. | Individual guide, slides 33–34. Final practice mock M6. |
| 09 · Viewing transformations | Label object, world, camera, normalized and screen coordinates. Trace a point and explain how the camera transform reverses the camera’s pose. | Individual guide, slides 26–27. |
| 10 · Rasterization theory | Sketch a triangle and a pixel sample. Explain what the barycentric weights tell you and why an overlapping fragment still needs a depth test. | Individual guide, slides 13–14. Final practice drill 8. |
| 11 · Rasterization implementation | Explain what changes from vertex to fragment to framebuffer. Compare why flat shading shows facets and why a small highlight can disappear with per-vertex lighting. | Final practice drills 8–9. |
| 12 · Perspective projection | Sketch a side view with the eye, near plane and half-angle. Use the supplied equation to find the near rectangle and explain how distance affects size. | Final practice drill 7 and mock M3. |
| 13 · Texture mapping | Distinguish interpolating UVs from filtering texels. Explain why a distant checkerboard can shimmer and how a mip level changes the sample. | Final practice drills 10–11 and mock M2. |
| 14 · Parametrization | Explain how pinned boundaries constrain free UVs. Distinguish flipped faces, nonlocal overlap and distortion using one chart sketch. | Final practice drill 12 and mock M5. |

## How to use the materials already in study

| Material reviewed | Role in your final preparation |
| --- | --- |
| Intro and Images, Linear Algebra | Use the examples to interpret alignment, orientation, colour and alpha. Explain the idea and work an example with the equation visible. Check the pixel-centre convention stated in each question. |
| C++ guide | Background for following assignments. Skim the data flow and what references accomplish if needed. Leave syntax drills, build flags and language trivia out of your final study blocks. |
| Ray Tracing, Procedural Synthesis, Spatial Data Structures | Work the prompts on ray hits, shadow intervals, the noise blend, safe distance steps and AABB traversal. Use sketches of the camera, light and boxes to explain boundary cases. |
| 2D Transformations, Viewing Transformations, Rasterization Theory and Implementation | Explain which space a position is in, why transform order matters, and how coverage, interpolation, depth and shading differ. The implementation deck’s callbacks are an example of the conceptual pipeline. |
| Perspective Projection, Texture Mapping, Parametrization and their three study sets | Use these for extra equation-in-context and diagram practice. The perspective study set uses signed camera coordinates for near and far planes. The combined guide’s frustum examples explicitly use a positive near **distance**. Both describe the same geometry. |
| [Older assignment-centred review deck](computer-graphics-final-exam-study.pptx) | Extra A3 practice on rays, light, reflection and noise. Its implementation checks belong with the assignment. Use its formula slides as references for its exercises, and trace the quantity each formula calculates. |
| Combined final guide and separate practice sheet | Use the final guide as the main review. Use the separate sheet for 12 topic drills and a six-question mixed mock with a separate answer key. |

### Conventions to check before calculating

- **Formula summaries.** Some individual decks still say to write the summaries from memory. Use the summaries as references while you practise applying and interpreting the equations. The instructor’s November 24 guidance governs the exam.
- **Depth direction.** The Lecture 09 orthographic example maps the near plane to +1. Some practice questions instead explicitly use smaller depth for nearer surfaces. Read the comparison rule in the question before deciding which fragment wins.
- **Pixel centre and camera signs.** Integer-centred grids and grids with a half-pixel offset both appear in the resources. Label that convention on your sketch. The Lecture 12 study set also distinguishes signed camera coordinates from a positive near-plane distance.
- **Texture filtering.** In bilinear filtering, blend each row with the horizontal fraction and blend the two rows with the vertical fraction. The Lecture 13 practice set flags the vertical-weight typo on the original slide.

### Match a sketch to the explanation

| Sketch | What to label | What it should explain |
| --- | --- | --- |
| Camera and field of view | Eye, centre line, image plane, near distance, half-angle and half-height | Why the right triangle uses half the full vertical field of view. |
| Shadow or reflection ray | Hit point, surface normal, ray directions, light and blocker | Why a blocker behind a point light does not block it, or which vector component a reflection reverses. |
| Ray and BVH | Parent and child boxes, ray direction, box entry and nearest triangle hit | Why a miss prunes a subtree and why a hit can still be a false candidate. |
| Rasterized triangle | Vertex labels, sample point, three weights and depth candidates | How coverage and interpolation use the same weights, and how depth resolves overlap. |
| UV chart | 3D seam, duplicated chart corners, pinned boundary and interior point | Why one 3D location can have several UVs and how the boundary constrains the interior. |

## Final self-check

- I can trace one ray from a pixel to the nearest hit, calculate the normal, and state when a light contributes.
- I can trace one triangle from object coordinates to pixel colour, including barycentric weights, depth and blending.
- I can explain the same distinction using an example: triangle versus parallelogram, BVH versus spatial partition, orthographic versus perspective, flat versus per-vertex shading, or texture filtering versus parametrization.
- I can carry out a small derivation with a supplied formula and check the result without remembering an entire matrix.
- I can explain how a mesh file, a normal, a UV coordinate, and a texel each enter the pipeline.
