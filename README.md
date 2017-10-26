# THREE.js-PathTracing-Renderer
Real-time PathTracing with global illumination and progressive rendering, all on top of the Three.js WebGL framework.

<h2>LIVE DEMOS</h2>

* [Geometry Showcase Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Geometry_Showcase.html) demonstrating some primitive shapes for ray tracing.

* [Billiard Table Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Billiard_Table.html) shows support for image textures (i.e. .jpg .png) being loaded and used for materials (the billiard table cloth and two types of wood texture images are demonstrated).

* [Cornell Box Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/CornellBox_DirectLighting.html) which renders the famous Cornell Box, but at ~60 fps!

For comparison, here is a real photograph of the original Cornell Box vs. a rendering with the three.js PathTracer:

![](readme-Images/measured.jpg) ![](readme-Images/CornellBox-Render0.png)

* <h4>Bi-Directional Path Tracing</h4> Nearly 20 years ago (Dec 1997), Eric Veach wrote a seminal PhD thesis paper on methods for light transport http://graphics.stanford.edu/papers/veach_thesis/  In Chapter 10, entitled Bi-Directional Path Tracing, Veach outlines a novel way to deal with difficult path tracing scenarios with hidden light sources (i.e. cove lighting, recessed lighting, spotlights, window lighting on a cloudy day, etc.).  Instead of just shooting rays from the camera like we normally do, we also shoot rays from the light sources, and then join the camera paths to the light paths.  Although his full method is difficult to implement on GPUs because of memory storage requirements, I took the basic idea and applied it to real-time path tracing of his classic test scene with hidden light sources.  For reference, here is a rendering made by Veach for his 1997 paper:

![](readme-Images/figure9b.jpg)

And here is the same room rendered in real-time by the three.js path tracer: <br>
* [Bi-Directional PathTracing Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Bi-Directional_PathTracing_ClassicTestScene.html) <br>
I had the above image only to go on - there are no scene dimensions specifications that I am aware of.  However, I feel that I have captured the essence and purpose of his demo room.  I think Veach would be interested to know that his scene, which probably took several minutes if not hours to render back in the 1990's, is now rendering real-time at 60 FPS on a web browser! :-D

For more intuition and a direct comparison between regular path tracing and bi-directional path tracing, here is the old Cornell Box scene but this time there is a blocker panel that blocks most of the light source in the ceiling.  The naive approach is just to hope that the camera rays will be lucky enough to find a light source:
* [Naive Approach to Blocked Light Source](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Compare_Uni-Directional.html) As we can painfully see, we will have to wait a long time to get a decent image!
Enter Bi-Directional path tracing to the rescue!:
* [Bi-Directional Approach to Blocked Light Source](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Compare_Bi-Directional_PathTracing.html) Like magic, the difficult scene comes into focus - in real-time!

* [Ocean and Sky Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Ocean_and_Sky_Rendering.html) which models an enormous calm ocean underneath a realistic physical sky. Now has more photo-realistic procedural clouds!

* [Water Rendering Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Water_Rendering.html) Renders photo-realistic water and simulates waves at 60 FPS. No triangle meshes are needed, as opposed to other traditional engines/renderers. In fact, not a single triangle was harmed during the making of this water volume! It is done through object/ray warping. Total cost: 1 ray-box intersection test!

* [Quadric Geometry Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Quadric_Geometry_Showcase.html) showing different quadric (mathematical) shapes (Warning: this may take 7-10 seconds to load/compile!)

<h3>Constructive Solid Geometry(CSG) Museum Demos</h3>

The following demos showcase different techniques in Constructive Solid Geometry - taking one 3D shape and either adding, removing, or overlapping a second shape. (Warning: these demos may take 10 seconds to load/compile!) <br>
All 4 demos feature a large dark glass sculpture in the center of the room, which shows Ellipsoid vs. Sphere CSG. <br>
Along the back wall, a study in Box vs. Sphere CSG: [CSG_Museum Demo #1](https://erichlof.github.io/THREE.js-PathTracing-Renderer/CSG_Museum_1.html) <br>
Along the right wall, a glass-encased monolith, and a study in Sphere vs. Cylinder CSG: [CSG_Museum Demo #2](https://erichlof.github.io/THREE.js-PathTracing-Renderer/CSG_Museum_2.html) <br>
Along the wall behind the camera, a study in Ellipsoid vs. Sphere CSG: [CSG_Museum Demo #3](https://erichlof.github.io/THREE.js-PathTracing-Renderer/CSG_Museum_3.html) <br>
Along the left wall, a study in Box vs. Cone CSG: [CSG_Museum Demo #4](https://erichlof.github.io/THREE.js-PathTracing-Renderer/CSG_Museum_4.html) <br>

Important note! - There is a hidden Easter Egg in one of the 4 Museum demo rooms.  Happy hunting!

<h3>Materials Demos</h3>

These demos showcase different materials possibilities: <br>
[Materials Demo #1](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Materials_Showcase_1.html) Refractive (glass/water) and ClearCoat (billiard ball/car paint) materials <br>
[Materials Demo #2](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Materials_Showcase_2.html) Cheap Volumetric (smoke/fog/gas) and Specular (aluminum mirror) materials <br>
[Materials Demo #3](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Materials_Showcase_3.html) Diffuse (matte wall paint/chalk) and Translucent (skin/balloons,etc.) materials <br>
[Materials Demo #4](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Materials_Showcase_4.html) Metallic (Gold) and shiny SubSurface scattering (polished Jade/wax candles) materials <br>

![](readme-Images/threejsPathTracing.png)

<br>
<h2>FEATURES</h2>

* Real-time interactive Path Tracing in your Chrome browser - even on your smartphone! ( What?! )
* First-Person camera navigation through the 3D scene.
* When camera is still, switches to progressive rendering mode and converges on a photo-realistic result!
* The accumulated render image will converge at around 1,000-2,000 samples (lower for simple scenes, higher for complex scenes).
* Direct lighting now makes images render/converge almost instantly!
* Both Uni-Directional (normal) and Bi-Directional path tracing approaches available for different lighting situations.
* Support for: Spheres, Planes, Discs, Quads, Triangles, and quadrics such as Cylinders, Cones, Ellipsoids, Paraboloids, Hyperboloids, Capsules, and Rings/Torii.
* Constructive Solid Geometry(CSG) allows you to combine 2 shapes using operations like addition, subtraction, and overlap.
* Basic support for loading models in .obj format (triangle and quad faces are supported, but no higher-order polys like pentagon, hexagon, etc.)
* Current material options: Metallic (mirrors, gold, etc.), Refractive (glass, water, etc.), Diffuse(matte, chalk, etc), ClearCoat(cars, plastic, billiard balls, etc.), Translucent (skin, leaves, cloth, etc.), Subsurface w/ shiny coat (jelly beans, cherries, teeth, polished Jade, etc.), Volumetric (smoke, dust, fog, etc.)
* Materials can now use Texture images which can be loaded, applied, and manipulated in the path tracer       
* Diffuse/Matte objects use Monte Carlo integration (a random process, hence the visual noise) to sample the unit-hemisphere oriented around the normal of the ray-object hitpoint and collects any light that is being received.  This is the key-difference between path tracing and simple old-fashioned ray tracing.  This is what produces realistic global illumination effects such as color bleeding/sharing between diffuse objects and refractive caustics from specular/glass/water objects.
* Camera has Depth of Field with real-time adjustable Focal Distance and Aperture Size settings for a still-photography or cinematic look.
* SuperSampling gives beautiful, clean Anti-Aliasing (no jagged edges!)
* Users will be able to use easy, familiar commands from the Three.js library, but under-the-hood the Three.js Renderer will use this path tracing engine to render the final output to the screen.

<h3>Experimental Works in Progress (W.I.P.)</h3>

The following demos show what I have been experimenting with most recently.  They might not work 100% and might have small visual artifacts that I am trying to fix.  I just wanted to share some more possible areas in the world of path tracing! :-) <br>

Rendering spheres, boxes and mathematical shapes is nice, but most modern graphics models are built out of triangles.  The following demo uses an .obj loader to load a model in .obj format (list of triangles) from disk and then places it in a scene to be path traced.  As of now, it runs too slow for my taste.  It still needs a BVH acceleration structure to speed things up greatly (I am currently investigating different approaches on the GPU). I am showing this because I wanted to demonstrate the ability of the three.js PathTracing renderer to load and render a model in one of the most popular model formats ever: <br>

* [.OBJ Model Loading Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/OBJ_Model_Loader.html)<br>

I now have a working BVH (Bounding Volume Hierarchy) builder.  It builds a nested set of bounding boxes to avoid having to test every single triangle in the scene. Scenes which used to render at 10 FPS are now rendering at 50-60 FPS! For BVH test purposes, I randomize the branch that the ray takes when it is traversing the array of Bounding Boxes.  Hence the following demo, which renders the triangle model (a vintage desktop DOS PC - ha ha) as more of a 'point cloud' than a solid object. This is because the rays are taking random branches since in WebGL 1.0, I can't keep a stack with dynamic indexing like Boxes[x].data where x is the correct branch. But at least the model is loading and rendering very quickly. I just have to figure out how to access the arrays of boxes somehow so that the ray always takes the correct branch, and backs up and takes the other fork if it fails.  In the meantime, enjoy this 'artistic' rendering, where it seems to ask, "What is real? Does the computer create the scene, or does the ray-tracing scene create the computer?"  I know, I know - programmer art! :D <br>

* [BVH Debugging Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/WIP_BVH_Debugging.html)<br>

This Demo renders objects inside a volume of gas/dust/fog/clouds(etc.).  Notice the cool volumetric caustics from the glass sphere on the left!: <br>

* [Volumetric Rendering Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Volumetric_Rendering.html) <br>

Some pretty interesting shapes can be obtained by deforming objects and/or warping the ray space (position and direction).  This demo applies a twist warp to the spheres and mirror box and randomizes the object space of the top purple sphere, creating an acceptable representation of a cloud (for free - no extra processing time for volumetrics!)
* [Ray/Object Warping Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Ray_Warping.html)<br>

Taking this object warping idea further, I have been experimenting with rendering deformable surfaces such as liquids. Each ray (1 of millions) gets its own personalized map of where the deformable surface is located in 3D space, depending on where the ray hits the original non-deformed bounding box / bounding shape.  I am quite pleased with the initial results - pixel-accurate smooth surfaces, no cracks, seams or facets as you sometimes get with traditional triangulated patches/meshes.  And best of all, the total computation cost is 1 initial bounding shape and 1 deformed/displaced shape of the same type!  This can be executed on the GPU in parallel, achieving real time realistic looking water movement at 60 FPS on desktop and 30 FPS on a smartphone!  Later I will experiment with rendering terrain such as hills and mountains, maybe borrowing some popular fractal fBm noise functions on sites like glslSandbox and ShaderToy.
* [Liquid (Fake) Simulation Demo](https://erichlof.github.io/THREE.js-PathTracing-Renderer/Liquid_Simulation.html)<br>

<h2>Updates</h2>

* October 26th, 2017: Texture images for materials are now supported!  Images stored on the server can be quickly loaded, applied to materials, and even manipulated in real time inside the path tracing loop. To see how to use texture images, check out the Billard Table demo above, then have a look at the source code to see how to setup, load, and apply the textures.  It's a little hacky right now because I'm still figuring out the best way to integrate the concept of a three.js 'material' and my path tracing 'material'.  It's not a direct 1 to 1 correspondence because although both materials have concepts of their own color and image texture properties, mine have to contain reflectance data so that path tracing rays can bounce of the materials correctly.  Also, in the near future I want to add support for normal maps (images that change the surface normals data) so that bumpy, rough, or scratchy surfaces will pop out in 3D more.  On the side, I'm still working on terrain (mountains) rendering from a heightmap texture image.  Going pretty well, but I need more FPS. GPU thread divergence among differnt rays (mountain rays on the lower half of the screen vs. sky rays on the upper half) is eating into the frame rate.  But visually it looks great - it's like you are transported to the himalayas!
* October 3rd, 2017: Major strides have been made in the Bi-Directional path tracing area.  Difficult scenes (due to hidden light sources) which used to take minutes if not hours to come into focus, are now running at 60 FPS and converging under a minute, sometimes within seconds! Check out the new Bi-Directional scene demos above. In Eric Veach's (co-inventor of the Bi-Directional method) original algorithm, he kept a stack of camera path data as well as light path data, then chose different combinations of those 2 paths, depending on the effeciency they had on desired visual effects of the particular scene at hand.  This is not well-suited for GPUs because of the memory stack requirements, so I simplified the full algorithm down to what I'm calling Quasi Bi-Directional path tracing.  Instead of keeping a stack of all the possible paths, I simply join the random camera path to the random light path at the end of the ray tracing loop.  It runs so fast that all the desired effects eventually come into focus, which makes it possible for real-time games in the future where the game character might be in a dimly lit room.  I might put my simplified real-time algorithm to the ultimate test and try to render this scene: https://erichlof.github.io/THREE.js-PathTracing-Renderer/readme-Images/Ref.png Eric Veach had to resort to his novel Metropolis Light Transport (MLT) to deal with this super-difficult lighting situation. Just for fun, I may want to see how my lowly quasi bi-directional method stacks up! ;-) 
* September 9th, 2017: I've had my head in the clouds all summer long - literally! :-D I finally got the hang of using rgb noise textures to build and path trace procedural clouds.  Check out the new clouds inside the OceanAndSky rendering demo.  Now it's starting to look convincing!  I am currently working on making procedural landscapes with this new technique I learned (after 3 months of trial and errors, more of the latter ha ha).  Once I get procedural landscapes going smoothly, I will turn my attention to using jpg and png textures and applying them to object materials to be rendered.  I've received a couple of recent requests for this feature.  Stay tuned!
* May 4th, 2017: I had a breakthrough with liquid/fluid rendering and simulation. Check out the new Water Rendering Demo!  These breakthroughs don't happen very often, especially for a hobbyist like me, but I was overjoyed at the realism and rendering speed of the new water simulation demo.  I first started out trying the more traditional bump-map/water-plane approach, but the illusion only works if you are at a good viewing angle - it quickly breaks down when you try to 'swim' in the liquid. I then started thinking 'outside the waterBox'(ha), and instead, I move the entire water box up and down for each ray, depending on where the ray strikes it. Each one of millions of rays gets its own personalized map of where the box is, depending on where the ray initially strikes the un-transformed box. The result is smooth, pixel-accurate, wavy water, with no facets or edges. Also you can swim underneath the surface, look upwards, and watch the above dry world bobble around with physically accurate refraction - give it a try! The wave motions are just simple sine wave functions that spit out Y values (wave-height) based on the X and Z coordinates as inputs.  If you wanted, you could easily use a displacement, bump, or noise texture to 'look up' the Y wave-height value depending on the X and Z coordinate of the ray-box intersection.  Next, I will explore rendering hills and mountains with the same technique, maybe with some fbm functions. I'll post something if it pans out!
* April 21st, 2017: Major rendering engine update across all demos - more FPS and more photo-realism!  Also I have a working BVH builder for triangle models!  Check out the 'BVH debugging' demo above. The BVH data structure has sped up triangle models greatly - I'm getting around 60 fps for low poly models under 1000 triangles! However, rendering them is another story: I've hit a wall with the current WebGL 1.0 shader language (GLSL):  It doesn't allow accessing an array with a variable, like you can easily do in other languages.  For example, vec3 myBoxesData[64];  int x = 13;  float correctNode = myBoxesData[x].  The statement with myBoxesData[x] fails under the current implementation of WebGL 1.0 (It must be a constant like '2' or something).  Hopefully this won't be an issue when Three.js moves over to WebGL 2.0, which does support dynamic indexing of arrays. But in the meantime, I'm trying to figure out a workaround. Also I've been experimenting on the side with rendering fluids like water, oil, milk, etc.  I'll post something as soon as I get it working! :)
* March 3rd, 2017: Complete overhaul of mobile joystick controls.  Now the controls on Cell Phones and Tablets have a smooth, fluid response.  Also I changed the look of the buttons to directional, which makes more sense in this fly-cam setting.  However, I left the vintage joystick arcade-style circular buttons code intact, but commented out, so if you want a character jump-action button, etc., you can just mix and match the button shapes to your liking! :-) <br>

<h2>TODO</h2>

* Add support for layered texture materials (diffuse, normal map, specular map, emissive map, etc.)
* Instead of scene description hard-coded in the path tracing shader, let the scene be defined using the Three.js library
* Debug BVH branching - figure out a way around dynamic array index ban in WebGL 1.0, or wait until 2.0 support in three.js
* Dynamic Scene description/BVH updating and streaming into the GPU path tracer via Data Texture. <br>

<h2>ABOUT</h2>

* This began as a port of Kevin Beason's brilliant 'smallPT' ("small PathTracer") over to the Three.js WebGL framework.  http://www.kevinbeason.com/smallpt/  Kevin's original 'smallPT' only supports spheres of various sizes and is meant to render offline, saving the image to a PPM text file (not real-time). I have so far added features such as real-time progressive rendering on any device with a Chrome browser, FirstPerson Camera controls with Depth of Field, more Ray-Primitive object intersection support (such as planes, triangles, and quadrics), and support for more materials like ClearCoat and SubSurface. <br>

This project is in the alpha stage.  More examples, features, and content to come...
