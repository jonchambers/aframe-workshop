# aframe-workshop

A-Frame is a library built on top of three.js and uses its own html tags to generate 3D objects and scenes. It uses an entity and component system: components can be added to an empty entity. In HTML terms, the entities are like the tags and the components are like the different attributes that you can add to tags.

A-Frame also includes it’s own inspector so you can edit in the browser. This doesn’t change the code so you’ll nee to copy and paste your changes from the browser to your code using the little copy icon at the top right of the inspector window.

To open it while viewing your scene:

<ctrl> + <alt> + i

To create a WebVR scene in the index file, we need to add the <a-scene> tag between the body tag:

```
<body>
  <a-scene>
  <!-- All A-Frame code goes here -->
  </a-scene>
</body>
```

All of our A-frame code will be added between the <a-scene> open and close tags.

To create shapes we can use the <entity> tag. Most of the primitive object like boxes and spheres include their own tags (a-box, a0sphere), but we'll be using the entity tag. The code below will generate a sphere. A-Frame creates a default camera that’s positioned at XYZ coordinates 0, 0, 0, so we want to move this sphere away from the camera via the z axis, position="x y z;”
  
```
<a-entity
      geometry="primitive: sphere;"
      radius = "1;"
      position="0 1.5 -4;">
</a-entity>
```
