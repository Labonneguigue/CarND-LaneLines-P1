# **Finding Lane Lines on the Road**

### Here is a brief description of the image processing pipeline I built to detect the lines on both sides of the lane a car is driving in.

---
<img src="test_image_output/solidWhiteRight.jpg" width="480" alt="Combined Image" />

[original]: test_images/solidYellowCurve.jpg "Original"
[yellow]: test_image_output/yellow.jpg "Yellow"
[white]: test_image_output/white.jpg "White"
[gray]: test_image_output/gray.jpg "Gray"
[canny]: test_image_output/canny.jpg "Canny"
[mask]: test_image_output/mask.jpg "Mask"
[hough]: test_image_output/hough_2.jpg "Hough"
[final_result]: test_image_output/solidYellowCurve.jpg "Final result"
[no_grey]: test_image_output/solidYellowCurve_noGrey.jpg "No grey"
[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Here are the few steps that each image goes through

My pipeline consists of of 9 steps. Let's see the result of each of them on this image.

![alt text][original]

1. I extract an image with only the yellow component.

![alt text][yellow]

2. I extract an image with only the white component.

![alt text][white]

3. I extract a grayscale image.

![alt text][gray]

4. I merge these 3 images into 1. It visually gives the same image as above.
5. I blur a little bit the image to smooth out the contours to enhance the result of the next step.
6. I detect the edges (strong gradient in the pixel values) using the canny edges algorithm.

![alt text][canny]

7. I mask the region of the image where I do not expect the lines to be.

![alt text][mask]

8. I perform a hough transform to detect where the lines are.

![alt text][hough]

9. I average, extrapolate and filter the lines I obtain before drawing them on the image with a slight transparency. Here is the final result.

![alt text][final_result]


### 2. Potential shortcomings with my current pipeline

I detect the lanes quite far but I do not have stability when the road color changes. The lanes go far off target on the challenge.mp4 video. My other implementation where I do not take into account the grayscale image and only rely on the white and yellow images is very robust but do not detect the lanes as far. Here is the output on the same image :

![alt text][no_grey]

I did not try to feed some video input where the car is changing lane. This would probably show how rigid my solution is (expecting a left and a right line).

I represent the lanes by straight lines. There is an obvious shortcoming to that representation: I do not extract information regarding the curve of both lines.

### 3. Suggest possible improvements to your pipeline

I have the problem that I do not detect the lines very far with the solution where I only use the yellow and white pixels of the image but since I have a very good stability and accuracy with this implementation, I could use that as "Ground Truth" and try to extrapolate both lines to detect further away with the input where I use the grayscale image.
