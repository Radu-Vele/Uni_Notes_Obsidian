# Initial information
- found on Moodle

> [!info] The app should have the feeling of a game (photorealistic representation of 3D objects) and the following requirements incorporated:
> 
> - ***1. interact*** with the objects and the camera (mouse and key inputs - implement `Camera.cpp`)
> - ***2. Animation***: specify a set of 3D points -> `interpolate` the camera position to go through all these points & change camera position (simple: linear interpolation, more complex: use the points as control points for a `Bezier` curve)
> - ***3. Light sources*** - one is directional, one is positional
> 	- Combine the influence from the 2 light sources 
> - ***4. Solid/Wireframe*** - call an openGL method to change the type of representation (somehow like 4th lab)
> - ***5. Smooth/polygonal surfaces*** - to have polygonal we should not interpolate the normals
> - ***6. Texture mapping & materials*** - pretty much what's implemented in the project core and that's it
> - ***7. Shadow mapping*** - for the directional light source only
> - ***8. Animate object components*** - animate subcomponents of the objects
> - ***9. Photorealism*** - choose some of the ideas of algorithms (collision detection, other light sources, )
> - ***10. Documentation*** - described
 
## Theme brainstorming

### Nature stuff:
- camping site with fire, some trees, tents, 🏕
- mountain top - Id like a lot ⛰ (a bit more difficult with terrain - climbing?)
	- birds, hikers

### Indoor:
- basketball court with a ball bouncing 🏀
- house of a person (many objects) - safer option, resources++ 🏚

## Notes from the last lab

### Blender tip:
- export the model for the landscape (static stuff)
- export the animated objects separately (treat them separately)
	- careful about the origin of the scene of objects (object that rotate and stuff will need to be translated to the origin of the system)

Resources:
- use blender images
- download stuff - careful to have them working (textures, coordinates specifications)