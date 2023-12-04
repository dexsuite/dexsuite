---
sidebar_position: 2
---

# Improvement Details

Here we document how we improve the robot models in each of the following aspect compared with the
original URDF file provided by manufacturer.

### Better collision mesh

All collision mesh are represented as stl or URDF primitives with simplified triangle meshes, i.e.
fewer vertices and
simpler edge connection. No self collision after loading into simulator.

### Better visual mesh

1. **Consistent mesh format.** All visual mesh are converted as `.obj` but not `dae` due to the
   inconsistencies of `dae`
   loader. For each robot model, we also provides a `glb` version with visual meshes stored
   in `glTF-2.0` format, which
   better support the Physically Based Rendering (PBR) material. Many simulators, such as IsaacGym
   and SAPIEN, can
   utilize the glb version to achieve superior visual results.
2. **Paint color for mesh.** We paint the color of the visual mesh based on the real robot, as well
   as other material
   parameters like specular and metalic. Although these parameters are estimated by human eyes, they
   looks reasonable
   and better than no color.
3. **No material tag to specify color.** The color of each visual mesh are stored in the mesh file
   rather without
   any `<material>` tag in the URDF. When both `obj`(sometimes the associated `mtl`)
   and `<material>` tag contains color
   information for a mesh, it is tricky to define which one can override the other. To avoid some
   conflicts, we remove
   all material tag in the URDF.

since different DAE loader may treat DAE differently, resulting inconsistent behavior across
different URDF parser.
For enhanced support of physically based rendering,
every URDF file in this repository is accompanied by a GLTF version of urdf,
which contains meshes in glb format, in addition to a standard urdf with obj mesh.

### Better inertia and joint parameters

### Uniform URDF parsing across diverse parsers

### Standardized frame convention

For all dexterous hands, the orientation are kept consistent across all dexterous hands. For right
hand, the x-axis is
forward, the y-axis the direction from litter finger to thumb, the z-axis is the direction from
wrist to fingertip of
middle finger.

### Added auxiliary links