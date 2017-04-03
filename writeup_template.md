# **Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 

Please see below the ouput images with a example of solidWhiteCurve.jpg of the steps.
1. Convert each image into a grayscale.
    ![alt tag] (https://github.com/ankit2grover/CarND-LaneLines-P1/blob/master/output_images_solidWhiteCurve/gray.jpg)
  
  
2. Converted grayscale image into blur for smoothening the image with kernel filter size as 5.
   ![alt tag] (https://github.com/ankit2grover/CarND-LaneLines-P1/blob/master/output_images_solidWhiteCurve/blurGray.jpg)
   
3.  Detected Edges using Canny Edges Detection Algorithm with low threshold and high threshold valus as 50, 150 respectively.
    ![alt tag] (https://github.com/ankit2grover/CarND-LaneLines-P1/blob/master/output_images_solidWhiteCurve/canny.jpg)

4.  Masked the Canny image with interested region.
    ![alt tag] (https://github.com/ankit2grover/CarND-LaneLines-P1/blob/master/output_images_solidWhiteCurve/regionMasked.jpg)
    
5. Detected interested lines from masked image and marked those lines with red color using Hough Lines Algorithm.
    ![alt tag] (https://github.com/ankit2grover/CarND-LaneLines-P1/blob/master/output_images_solidWhiteCurve/houghLinesImage.jpg)
    
6.  Combined original image with the lines image to see the result image.
    ![alt tag] (https://github.com/ankit2grover/CarND-LaneLines-P1/blob/master/output_images_solidWhiteCurve/finalImage.jpg)
    
Similarily, I read each image in the pipeline using pipeline_image_process() function and process each image with same steps as mentioned above. At last, saved each image in the test_output_images directory. I have submitted test_output_images directory also that is containing the result of all the images in the pipeline.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by computing the slope to differentiate between left and right line segments. 

Negative slope is left line segments and positive is right line segments.

Then, calculated the mean of all the points in the left and right line segments in two separate arrays.

Computed mean slope of the mean points and then considered extrapolated Y-axis points as topY (325 px) and bottomY (img.shape[0] px).

At last, using the function (y2-y1_mean)/(x2-x1_mean) = slope_mean, computed extrapolated xtop and xbottom points.

Also, test_videos_output containing result of both test videos as well as result of the optional challenge.



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be that sometimes detected red line is having marginal error with original dashed lane lines and that error is very less but it can definitely affect on real time driving.

Another shortcoming could be on the sharp curves detected lane lines will have more error with original lane lines.

Also, I have selected extrapolated top point of the image as 325 and that value should be automatically picked up as per the focal length of the camera.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be update the top point value everytime as car is moving so that it shows less error on the curves.

Like our eye only focus on the less distance on sharp curves, similarily top point value also should be less on the sharp curves.
