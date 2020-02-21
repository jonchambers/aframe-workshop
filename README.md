# aframe-workshop

A-Frame is a library built on top of three.js and uses its own html tags to generate 3D objects and scenes. It uses an entity and component system: components can be added to an empty entity. In HTML terms, the entities are like the tags and the components are like the different attributes that you can add to tags.

A-Frame also includes it’s own inspector so you can edit in the browser. This doesn’t change the code so you’ll nee to copy and paste your changes from the browser to your code using the little copy icon at the top right of the inspector window.

To open it while viewing your scene:

ctrl + alt + i

## Creating a scene
To create a WebVR scene in the index file, we need to add the a-scene tag between the body tag:

```
<body>
  <a-scene>
  <!-- All A-Frame code goes here -->
  </a-scene>
</body>
```

All of our A-frame code will be added between the <a-scene> open and close tags.

## Creating a shapes, skybox and text
To create shapes we can use the <entity> tag. Most of the primitive object like boxes and spheres include their own tags (a-box, a-sphere), but we'll be using the entity tag. The code below will generate a sphere. A-Frame creates a default camera that’s positioned at XYZ coordinates 0, 0, 0, so we want to move this sphere away from the camera via the z axis, position="x y z;”
  
```
<a-entity
  geometry="primitive: sphere;"
  radius = "1;"
  position="0 1.5 -4;">
</a-entity>
```
To change the skybox color we can use color, images or video. We'll look at how to add an image and video below. 

This will add a color to our skybox:
```
<a-sky color="#a442f4"></a-sky>
```
This will add text:
```
<a-text 
  value="Hello!" 
  color="#111" 
  position="0 2.5 -2" 
  align="center">
</a-text>
```
## Adding images and video

To add image and video textures we can use the assets tag to keep things organized.

```
<a-assets>
  <img id="skyTexture" src=“images/starmap.jpg”>
  <img id="io" src=“images/io.jpg”>
  <video id="city" autoplay loop="true" src=“video/city.mp4"></video>
  <video id=“mountain" autoplay loop="true" src=“video/mountain.mp4"></video>
</a-assets>
```
We can then use the image and video asset ids to add the textures to our objects and skybox.

To the Skybox:
```
<a-sky src="#skyTexture"></a-sky>
```
To a sphere:
```
<a-entity
  geometry="primitive: sphere;”
  radius = “1;"
  position="0 1.35 -4;”
  material="src: #io”>
</a-entity>
```
Adding a video element to the scene:
```
<a-video src="#mountain" width="16" height="9" position="0 0 -10”></a-video>
```

Adding a 360 Video as skybox:

```
<a-videosphere src=“#city"></a-videosphere>
```
## Adding 3D models to your scene
Adding models to A-Frame requires that you use .obj or .gltf formats. OBJ files are more common, but GLTF are made for using in the browser. Both will work though. The code below should be added in your assets tag like we did with the images and video. 

Loading the obj with its mtl material file in the a-assets tag:

```
<a-asset-item id="tower-obj" src="models/model.obj"></a-asset-item>
<a-asset-item id="tower-mtl" src=“models/materials.mtl"></a-asset-item>
```

Loading a gltf:
```
<a-asset-item id="tower-gltf" src="models/model.gltf"></a-asset-item>
```

Then Load them using an entity.

Obj:
```
<a-entity 
  obj-model="obj: #tower-obj; mtl: #tower-mtl"
  position="0 0 0"
  rotation="0 0 0"
  scale="1 1 1">
</a-entity>
```
GLTF:
```
<a-entity 
  gltf-model="#tower-gltf"
  position="0 0 0"
  rotation="0 0 0"
  scale="1 1 1">
</a-entity>
```
## Animating
Animation in A-frame requires the use of the animation component. The sphere below with the texture of a-frame animationIo will rotate 360 degrees on it’s y axis. It will take 15000 milliseconds and loop.
```
<a-entity 
  geometry="primitive: sphere;"
  radius="1;"
  material="src: #io"
  position="1 1.5 -3"
  animation="property: rotation;
             to: 0 360 0;
             dur: 15000;
             easing: linear;
             loop: true;">
</a-entity>
```
More on animations can be found [here](https://aframe.io/docs/1.0.0/components/animation.html)

## A-Frame Registry
A bunch of different libraries that expand the functionality of A-Frame are available through its registry:

[https://aframe.io/aframe-registry/](https://aframe.io/aframe-registry/)

Some useful ones:

[Physics](https://www.npmjs.com/package/aframe-physics-system)

[Particle System](https://www.npmjs.com/package/aframe-particle-system-component)

[Environments](https://www.npmjs.com/package/aframe-environment-component)

[Text Geometry](https://www.npmjs.com/package/aframe-text-geometry-component)

The [Extras](https://github.com/donmccurdy/aframe-extras) library includes different controller navigation.


To add basic physics to our project, you’ll need to include the physics library. Then in your a-scene tag add physics component:
```
<a-scene physics>
```
You can then add dynamic-body or static-body to your objects. Static bodies will include collision information, but will stay in the same place in the scene. The box below will fall when the page is loaded:
```
<a-entity dynamic-body
  geometry="primitive: box;"
  position=".75 4 -3;"
</a-entity>
```

To add particle systems to our project, you’ll need to include the particle system library.

Then, create an entity that includes a particle system. Just an FYI, these are pretty processor intensive.
```
<a-entity 
  position="0 2.25 -15" 
  particle-system="preset: snow; size:5">
</a-entity>
```

To add an environment to your project, you’ll need to include the environment component library.

Then, create an entity that includes an environment preset.
```
<a-entity environment="preset: tron"></a-entity>
```

You can also add 3D text to you project by using the Text Geometry component library:
```
<a-entity 
  text-geometry="value: Hello World!” 
  position="0 5 -2">
</a-entity>
```
## VR Controllers 
To add VR movement controls we need to include the Extras library. Then we need to override our default camera and create a camera rig entity and embed a camera inside it:
```
<a-entity id="cameraRig" wasd-controls movement-controls>

        <a-entity camera look-controls position="0 1.7 0"></a-entity>

</a-entity>
```
Adding the wasd-controls will allow for browser based navigations while adding the movement-controls will allow for basic VR navigation 

