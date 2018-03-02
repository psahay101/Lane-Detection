# **Finding Lane Lines on the Road**





---**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied gaussian blur to reduce the noise. Then we would apply an edge enhancer tool called as canny to bring out all the main edges. Now there are various parameters in this canny edge tool which can be adjusted so that only the main edges are enhanced. After this we darken the region which is not of our concern by making a triangle out of three chosen vertices in a way which entraps the road or lane which needs to be marked. So after this process we are left with a totally black image except for the two lane lines which are to be colored red. Now for this we use a tool called as the Hough transform. Even this tool has various parameters which are to be adjusted in order to get our desired result which for us is a well connected two clear red lines. After this we overlay this image on top of the normal or the actual image of the lane so finally we end up with the red marked lanes on the actual image. By the way for overlaying the tool used is a weighted add method of open cv.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by defining the slopes and intercepts of all the lines in the left and right lanes and then taking their median to find the respective slopes and intercepts for the left and right lanes. After that we find the minimum and maximum values of x for the corresponding min and max values using the respective slope and intercept for both left and right sides. after we have the x and y min, max for both left and right lanes we draw the lines using the cv2.line function on top of the image.

If you'd like to include images to show how the pipeline works, here is how to include an image:
First open the directory and store it as a variable. After that use for all the images in that variable kind of a loop inside which you can define all the previous operations which are defined in the first paragraph to finally obtain another modified image which by the way we can save into the same directory if needed.




### 2. Potential shortcomings with my current pipeline


One potential shortcoming would be what would happen when the lane lines are very thin then the edge tool might not consider it as a line at all.

Another shortcoming could be when the image changes drastically. That means if the lane moves out of the region of interest defined by us then the edges will be removed and the lane markings will go away.

One more scenario where this program could fail is if some cars block the lane lines so the edges won't be detected.
Another failure could be when the lane curves inwards or outwards then the straight lines won't be possible.


### 3. Possible improvements to my pipeline

A possible improvement would be to assume that the distance between the two lines would always be the same and if one lane is visible clearly then we can draw the other one even if the other lane is being mostly blocked that is even when small bits of edges are present, it can be assumed with a confidence that there is a presence of another line.

Another potential improvement could be to make the region of interest dynamic which means that the triangle's area could be increased in a scenario where one or more edges are not being detected. There can be a scenario where due to change in shape of the road( for example a sharp turn, the lanes) one or both the lines could get out of the picture so in that case the triangle can either be dynamically shifted to search for two lines with similar distances in the beginning of the horizon as that will usually be a constant as roads have usually a fixed distance between the lanes.
