# assets/clothing/

GLB clothing meshes that mount on a body anchor (usually Chest or Back).
The app ships placeholder geometry for the activist vest, etc. To swap in a
real GLB later, call this in index.html:

    attachGLB('Chest', 'activist-vest.glb');

The mesh becomes a child of that anchor and follows the body and animation.
