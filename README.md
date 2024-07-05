# Erik Haliewicz's personal github page.

# Projects

## Voxel renderer (2023-current)

### A CPU powered (no GPU!) 5DOF voxel renderer, supporting arbitrary voxel geometry, transparency, deferred shading, and horizon fogging.  5DOF means that the camera can rotate left and right, roll left and right, move up/down, left/right, forward/back.  It cannot do correct pitch up/down (the rendering algorithm is a distant cousin of the voxelspace comanche style voxel renderer), but it can shear the projected voxels to approximate the affect in screen-space.


### [Source code](https://github.com/ehaliewicz/voxel).

#### A foggy morning on rocket island

![A foggy morning on rocket island](rocket_island.png)

#### Voxel city

![Voxel city](vox_city.png)


### While working on this project, to make up for the lack of performance relative to a GPU, I experimented with optimizing data-structures for faster access via the CPU caches, using techniques like swizzling (voxel columns that are nearby in 3d-space are nearby in memory addresses as well), and using SoA style techniques and bit-packing to reduce bandwidth costs and improve cache-hit rate.
### I also wrote multi-threading code to process different chunks of the framebuffer in parallel, as well as used SIMD intrinsics (AVX2) to greatly improve the overall performance of the renderer after cache optimizations were introduced.
### As a result of these optimizations, the renderer runs at around 60-100fps at 1080p, depending on your CPU and the scene being rendered.

### Deferred shading is implemented by storing diffuse color and transparency coverage, world voxel position, (compressed) normal map into separate buffers while the voxel world is being traversed.  
### When transparent voxels are encounted, we update the values in the opaque color and transparency coverage buffer, but aside from that case each pixel is only drawn to once. 
### A second pass does a single linear pass over the output buffer pixels, using AVX2 to load and process the pixel information to rotate, light, and blend up to 8 pixels at once.  




## Manifold (2020-current)

### A project to create an advanced 2.5D Graphics engine and map creation toolkit, for Sega Megadrive/Genesis.

### [Source code](https://github.com/ehaliewicz/manifold).

#### A dark hallway
![A dark hallway](manifold_1.png)

#### A key in the room beyond
![ A key in the room beyond](manifold_0.png)

## Language Immersion Time Tracker (2022-2023)

### I was dissatisfied with existing tools for time tracking, so I decided to make my own.  Can be used for any kind of time tracking, but specifically tuned for my language learning needs.

### The backend is powered by python, django and postgres.  For the frontend, I avoided typescript, using javascript, preact, and htm so no builds were required and page load times were kept minimal.  

### This project does just about everything I need now, and is no longer under active development, aside from rare bugfixes.

### [Source code](https://github.com/ehaliewicz/time-tracker).

#### Daily todo list UI
![Daily todo list UI](todo_list_0.png)

#### Stats UI
![Stats UI](todo_list_1.png)



