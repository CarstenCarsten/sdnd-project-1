#**Finding Lane Lines on the Road** 

##Carsten finds lane lines on the road

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Seperate between the right and the left lane
* create images and videos to proof you lane finding works


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied a gaussian blur to the picture to smooth out small image imperfections, and other extreme image values.  After that the canny algorithm was applied to find the edges in the picture. Next, I extracted the lower half of the picture, where the road normaly should be. This helps in removing edges from the picture that are not the lane lines. Now I used the hough_lines algorithm to find long lines in the edges of the picture.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:

1. I calculate the slope (m) of the line, if the slope is too flat or too steep, I ignore the line.
2. I calculate the y-intercept point (b) of the line, so that I can basically use y=mx+b transformed to x=(y-b)/m to draw a line from the bottom of the picture to the horizon, the lower 2/5 of the picture.
3. If the slope is smaller than zero, the line goes from the left to the right, it has to be the left lane. If the slope is bigger than zero, the line goes from the right to the left. That has to be the right line.
4. Then I calculate the distance of the points, to find the longest line.
5. Then I only draw the longest left and the longest right line.

###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the car type changes. If the video is moved higher or lower on the road, the extraction of the lower part of the image would be bad.

Another shortcoming could be the detection of curves, currently only straight lines are implemented.

As the challenge video shows, in some light and shadow situation, the lane line is not the part with the highest gradient.
###3. Suggest possible improvements to your pipeline

A possible improvement would be to smooth out or average the x and y coordinates of the left and right lines. This would improve the "jumpiness" of the lines, and would smooth out found paralell lines.

Another potential improvement could be to work with a distance between the left and the right line. If the distance between both lines suddendly increases significantly, perhaps the longest line is not the lane line anymore.

###4. Example videos / results

[Solid White Right](test_videos_output/solidWhiteRight.mp4)
[Solid Yellow Left](test_videos_output/solidYellowLeft.mp4)
[Challenge](test_videos_output/challenge.mp4)
