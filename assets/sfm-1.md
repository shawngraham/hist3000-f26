---
layout: default
title: sfm-1
nav_exclude: true
---

Photogrammetry is the process whereby multiple photographs of an object are stitched together to make a 3d model of the object; the photographs are then draped over the model to make it photorealistic. Because of the physics of photography (focal distances of lenses and so on) a computer can calculate the relative positioning of overlapping points it identifies in multiple photographs, and with a bit of trig it works out the points-in-space. Then it joins these points up by connecting to the nearest neighbouring points, creating a series of triangles or ‘mesh’.

A common digital format then for these models is a folder with a .obj file describing the geometry of the object, a .png file with all of the texture information, and a .mtl file that tells the computer how to drape the texture onto the model. Services like [sketchfab.com](https://sketchfab.com) let you upload a zip file of such a folder, and then display or annotate the object. Here’s one I did of a gravestone of one of the Moodie family burials:

<div class="sketchfab-embed-wrapper"> <iframe title="Gravestone2" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" allow="autoplay; fullscreen; xr-spatial-tracking" xr-spatial-tracking execution-while-out-of-viewport execution-while-not-rendered web-share src="https://sketchfab.com/models/c287761136a8421ca9856edf8efd595e/embed"> </iframe> <p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;"> <a href="https://sketchfab.com/3d-models/gravestone2-c287761136a8421ca9856edf8efd595e?utm_medium=embed&utm_campaign=share-popup&utm_content=c287761136a8421ca9856edf8efd595e" target="_blank" rel="nofollow" style="font-weight: bold; color: #1CAAD9;"> Gravestone2 </a> by <a href="https://sketchfab.com/electricarchaeo?utm_medium=embed&utm_campaign=share-popup&utm_content=c287761136a8421ca9856edf8efd595e" target="_blank" rel="nofollow" style="font-weight: bold; color: #1CAAD9;"> electricarchaeo </a> on <a href="https://sketchfab.com?utm_medium=embed&utm_campaign=share-popup&utm_content=c287761136a8421ca9856edf8efd595e" target="_blank" rel="nofollow" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a></p></div>

The general process runs like this:

+ image capture: take overlapping images; you want a high degree of overlap. Knowing the ‘interior and exterior’ orientation of the camera - its internal arrangements, including lens distortion, focal length and so on from the metadata bundled with the image, allows software to work out the position of the camera with regard to the points of overlap in the images.
+ image matching: tie points are matched and camera orientations are deduced
+ dense point cloud generation. The intersection of rays then allows us to work out the location of these points in space
+ secondary product generation
+ analysis / presentation

**We're not making models _just yet_**. Rather, I want you to take both video and photos of a gravestone that interests you.

For the video, walk around the gravestone/object such that you capture a view of it from its bottom third, its middle third, and its top third (so go around it three times). 

For the photos, you want to make sure you have a significant amount of overlap between photos; 24 or so will do the trick. Again, make sure that you get coverage from the bottom, middle, and top as best you can. Notice how taking multiple photographs, from multiple angles, really forces you to *look* at the object... what do you notice?

We'll come back to these photos later in the term (in week 10) to try to make a model from them; I will walk you through a notebook that shows how the process all works.  

{: .note } 
If you're interested, you can sign up for a free account with [Polycam.com](https://poly.cam/) and load your photos / video into their service and get very good results. Be careful and avoid signing up for any of their paid services, at least for the purposes of this course; their pop-ups encouraging you to sign up for pro accounts can be closed. 

## Handheld 3d Scanner

We have a handheld hybrid 3d scanner that uses both photography and lasers to create 3d representations of objects, and a small structured-light scanner. You will have an opportunity to use both during this class. We will try the hybrid scanner at the Billings Estate on some of the damaged gravestones. There is an art, a knack, to using these devices.