# CS 194-26 Project 5: \[Auto\]Stitching Photo Mosaics

## Project 5A: Image Warping and Mosaicing

### Part A1: Shooting Pictures
For this project, I decided to try and stitch a mosaic of the living room of the house I rent in Berkeley. I took the photos by placing my phone on a tripod and rotating the tripod to 5 different angles. I made sure to use AE/AF lock, although there are still slight lighting differences in the resulting photos.

<table>
  <tr>
    <td> <img src="p1_website_imgs/0.png" alt="Start image 0" width="200"/> </td>
    <td> <img src="p1_website_imgs/1.png" alt="Start image 1" width="200"/> </td>
    <td> <img src="p1_website_imgs/2.png" alt="Start image 2" width="200"/> </td>
    <td> <img src="p1_website_imgs/3.png" alt="Start image 3" width="200"/> </td>
    <td> <img src="p1_website_imgs/4.png" alt="Start image 4" width="200"/> </td>
  </tr>
</table>

### Part A2: Recovering Homographies

In order to stitch images, we have to be able to compute the homography from one image to another. The math for this is briefly explained in the image below, since Github pages doesn't support LaTeX.

<img src="p1_website_imgs/homography_math.png" alt="Homography math from LaTeX" width="1000"/>

### Part A3: Warping Images

With the homography recovery function implemented, the next step was to try rectifying images. My results are shown below.

<table>
  <tr>
    <td> Before rectification </td>
    <td> <img src="p1_website_imgs/cube.png" alt="Cube before rectification" width="300"/> </td>
    <td> <img src="p1_website_imgs/gpu.jpg" alt="3080 before rectification" width="500"/> </td>
  </tr>
  <tr>
    <td> After rectification </td>
    <td> <img src="p1_website_imgs/cube_rectified.png" alt="Cube after rectification" width="300"/> </td>
    <td> <img src="p1_website_imgs/gpu_rectified.png" alt="3080 after rectification" width="500"/> </td>
  </tr>
</table>

We can see the results are pretty good! The cube does look slightly weird, as a normal top-down view centered on the cube wouldn't allow us to see the sides of the cube, but this is normal when applying a homography, as the transformed image is actually imagined from the viewer looking down at a point to the bottom-left of the cube.

### Part A4: Blending Images into a Mosaic

Now that we know our image warping works, we can work on blending images into a mosaic. This was done by first computing the homography matrix from the source image to the destination image. Then, a second homography was computed to transform the images into a third frame in which neither image had any part cut off. The source image would have both the first and second homographies applied to it by composing the two homographies, and the destination image would only have the second homography applied to it. On the sample images 0 and 1, this gave the following results.

<table>
  <tr>
    <td> Before warping </td>
    <td> <img src="p1_website_imgs/0.png" alt="Image 0 before warping" width="500"/> </td>
    <td> <img src="p1_website_imgs/1.png" alt="Image 1 before warping" width="500"/> </td>
  </tr>
  <tr>
    <td> After warping </td>
    <td> <img src="p1_website_imgs/left.png" alt="Image 0 after warping" width="500"/> </td>
    <td> <img src="p1_website_imgs/right.png" alt="Image 1 after warping" width="500"/> </td>
  </tr>
</table>

For blending, I did a simple blend of taking half of each image for the overlapping regions. The resulting alpha channels and final results are shown below

<img src="p1_website_imgs/simple_blend.png" alt="Blending alphas" width="1000"/>
<img src="p1_website_imgs/merged.png" alt="Resulting image" width="1000"/>

This blending worked alright, although there are still clear seams due to slight differences in lighting. However, the images do line up quite well.

Iteratively using this method, I was able to blend all 5 images into a mosaic, shown below.

<img src="p1_website_imgs/mosaic.png" alt="Mosaic" width="1000"/>

The result is pretty good, although you can see some blurriness in the center due to our handpicked points being imperfect. However, the next part of the project fixes this problem through automatic matching feature detection!

## Project 5B: Feature Matching for Autostitching

### Part B1: Detecting Corner Features

### Part B2: Extracting Feature Descriptors

### Part B3 Matching Feature Descriptors

### Part B4: RANSAC

### Part B5: Autostitching Mosaics
