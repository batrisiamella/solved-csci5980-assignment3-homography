Download Link: https://assignmentchef.com/product/solved-csci5980-assignment3-homography
<br>
Figure 1: (a) You will use the vanishing points in a single image to calibrate your cameras. (b) You will use multiple images of checkerboard patterns to calibrate your camera.

You will calibrate your camera (focal length, principal points, and lens distortion parameters).

<strong>Write-up:</strong>

<ul>

 <li>(Single Image Calibration) Take a single image where you can estimate three vanishing points <strong>v</strong><em><sub>X </sub></em><sub>inf</sub>, <strong>v</strong><em><sub>Y </sub></em><sub>inf</sub>, and <strong>v</strong><em><sub>Z </sub></em><sub>inf </sub>as shown in Figure 3(c). Compute <em>f</em>, <em>p<sub>x</sub></em>, and <em>p<sub>y </sub></em>using the vanishing points.</li>

 <li>(Multiple Image Calibration) Print out the checkerboard pattern as shown in Figure 1(b) (<a href="http://www-users.cs.umn.edu/~hspark/CSci5980/code/pattern.pdf">http://www-users.cs.umn.edu/</a><a href="http://www-users.cs.umn.edu/~hspark/CSci5980/code/pattern.pdf">~</a><a href="http://www-users.cs.umn.edu/~hspark/CSci5980/code/pattern.pdf">hspark/CSci5980/code/pattern.pdf</a><a href="http://www-users.cs.umn.edu/~hspark/CSci5980/code/pattern.pdf">)</a>. Derive <em>f</em>, <em>p<sub>x</sub></em>, and <em>p<sub>y </sub></em>based on homographies from multiple images (at least 5 images). Compute the intrinsic parameters by solving the least squares system.</li>

 <li>(MATLAB Toolbox Calibration) Use the existing MATLAB Calibration Toolbox</li>

</ul>

<a href="https://www.vision.caltech.edu/bouguetj/calib_doc/">(</a><a href="https://www.vision.caltech.edu/bouguetj/calib_doc/">https://www.vision.caltech.edu/bouguetj/calib_doc/</a><a href="https://www.vision.caltech.edu/bouguetj/calib_doc/">)</a> to compute the intrinsic parameters (at least 20 images from different views). Verify the estimate with your solutions in (1) and (2).

<h1>1             Rotation Interpolation</h1>




(c) Interpolated View

Figure 2: Using two images of pure rotation (a and b), you will generate interpolated view by sampling rotation (c)

In HW 2, we generate a panoramic image from multiple images. In this problem, you will use two images of pure rotation (Figure 2(a) and 2(b)) to generate many views by interpolating between rotations as shown in Figure 2(c).

<strong>Write-up:</strong>

<ul>

 <li>Compute the pure rotation, R<strong><sup>R</sup></strong><sub>L </sub>from the homography between two images, <sup>R</sup><strong>H</strong><sub>L</sub>.</li>

 <li>Interpolate between two rotations, , from <strong>I</strong><sub>3 </sub>(Left image) to <strong>R </strong>(Right image) where <em>N &gt; </em>20 is the number of interpolated rotations using SLERP.</li>

 <li>Generate interpolated images similar to Figure 2(c).

  <ul>

   <li>Given <em><sup>i</sup></em><strong>R</strong><sub>L</sub>, compute homography from Left image to the interpolated image, <em><sup>i</sup></em><strong>H</strong><sub>L </sub>and warp it, im1 = ImageWarping(imageLeft, <em><sup>i</sup></em><strong>H</strong><sub>L</sub>).</li>

   <li>Compute homography from Right image to the interpolated image, i.e., <em><sup>i</sup></em><strong>H</strong><sub>R </sub>=<em><sup>i </sup></em><strong>H</strong><sup>R</sup><sub>L</sub><strong>H</strong><sup>−</sup><sub>L</sub><sup>1</sup>. Warp image, im2 = ImageWarping(imageRight, <em><sup>i</sup></em><strong>H</strong><sub>R</sub>).</li>

   <li>Composite two images based on distance, imInterpolated = w*im1+(1-w)*im2 where w is weight, inversely proportional to the distance.</li>

  </ul></li>

</ul>

<h1>2             Tour into Your Picture</h1>

Figure 3: (a) Given a single image taken by a cellphone, you will navigate into the image. (b) You rectify the image such that the Y axis of the camera aligns with the surface normal of the ground plane. (c) You define the five principal planes using vanishing points. (d) A 3D box can be texture mapped.

Take an photo with your camera of a scene where you can observe the Z vanishing point. You will virtually tour into your photo that creates 3D sensation.

<strong>Write-up:</strong>

<ul>

 <li>Rectification: Rectify your image such that the surface normal of the ground plane is aligned with the Y axis of your camera using the homography between ground plane and the camera. Derive and compute the homography for the rectification. Visualize rectified image similar to Figure 3(b).</li>

 <li>Z vanishing point: Given the rectified image, derive and compute the Z vanishing point, <strong>p </strong>(Figure 3(c)) using the four edges from the ground and ceiling planes using linear least squares (the intersection of four lines), i.e., <strong>Ax </strong>= <strong>b</strong>.</li>

 <li>3D box generation:

  <ol>

   <li>Define the four corners (<strong>u</strong><sub>11</sub>, <strong>u</strong><sub>12</sub>, <strong>u</strong><sub>21</sub>, <strong>u</strong><sub>22</sub>) of the purple plane (Figure 3(c)) in the image.</li>

   <li>Define the depth of the four corner, e.g., <em>d</em>=1 and compute the 3D locations of the corners, <strong>U </strong>= <em>d</em><strong>K</strong><sup>−1</sup><strong>u</strong>.</li>

   <li>Express the 3D locations of frontal plane, <strong>V</strong><sub>11</sub>, <strong>V</strong><sub>12</sub>, <strong>V</strong><sub>21</sub>, and <strong>V</strong><sub>22 </sub>using <em>d</em>, <strong>p</strong>, <strong>K</strong>, <strong>u</strong>11, <strong>u</strong>12, <strong>u</strong>21, <strong>u</strong>22, <strong>v</strong>11, <strong>v</strong>12, <strong>v</strong>21, <strong>v</strong>22.</li>

   <li>Express a 3D point, <strong>X</strong>, in the 3D plane (<strong>U</strong><sub>11</sub>, <strong>U</strong><sub>12</sub>, <strong>U</strong><sub>21</sub>, and <strong>U</strong><sub>22</sub>), using two parameters, e.g., <strong>X </strong>= <strong>a</strong><sub>1</sub><em>µ</em><sub>1 </sub>+ <strong>a</strong><sub>2</sub><em>µ</em><sub>2 </sub>+ <strong>a</strong><sub>3</sub>. Apply this for the rest four planes.</li>

  </ol></li>

 <li>Homography mapping:

  <ol>

   <li>Derive and compute the homography per plane to the rectified image, i.e., <em><sup>s</sup></em><strong>H</strong><sub>plane1</sub>, <em>s</em><strong>H</strong>plane2, <em>s</em><strong>H</strong>plane3, <em>s</em><strong>H</strong>plane4, <em>s</em><strong>H</strong>plane5.</li>

  </ol></li>

</ul>

 <em>µ</em><sub>1 </sub>

<em>Hint</em>: <em>λ</em><strong>u </strong>= <strong>KX </strong><strong> a                                       H</strong>plane  <em>µ</em>2 .

1

<ol start="2">

 <li>Derive and compute the homography per plane to a target image of pure rotation about Y axis of the camera with 20 degree (<em>t</em><strong>H</strong>plane1, <em>t</em><strong>H</strong>plane2, <em>t</em><strong>H</strong>plane3, <em>t</em><strong>H</strong>plane4, <em><sup>t</sup></em><strong>H</strong><sub>plane5</sub>). Derive and compute the homography from the rectified image to the target image. <em>Hint</em>: <em>t</em><strong>H</strong><em>s </em>=<em>t </em><strong>H</strong>plane <em>s</em><strong>H</strong>−plane1 .</li>

 <li>Derive and compute the homography per plane to a target image of pure translation along Z axis of the camera with 0<em>.</em>2<em>d</em>. Derive and compute the homography from the rectified image to the target image.</li>

</ol>

(4) Generate camera trajectory by interpolating rotation and translation (at least 5 discrete rotation and translation) and generate a video of navigation.