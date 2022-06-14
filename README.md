# Python-class-121
invisible cloak

create the invisible cloak using an image processing technique called Color detection and segmentation. In order to make this project, you’ll need a single-color cloth. The cloth should not contain any other color visible. Here we are using a green cloth to develop this python project.


Color detection is a technique where we can detect any color in a given range of HSV color space.

Image segmentation is the process of labeling every pixel in an image, where each pixel having the same label shares certain characteristics.

----------------------------------------------

Steps to Build Invisible Cloak OpenCV Project:
Now we have everything ready. Below are the steps to create invisible cloak:

Import necessary packages and Initialize the camera.
Store a single frame before starting the infinite loop.
Detect the color of the cloth and create a mask.
Apply the mask on frames.
Combine masked frames together.
Removing unnecessary noise from masks.
---------------------------------------------------------------------------------------

Step 1 – Import necessary packages and Initialize the camera:

Explanation:

Using import, we imported the required libraries
To access the camera, we use the method cv2.VideoCapture(0) and set the capture object as cap.

--------------------------------------------------------------------------------------------------------------

Step 2 – Store a single frame before starting the infinite loop:

Explanation:


cap.read() function captures frames from webcam.
2-second delay between two captures are for adjusting camera auto exposure
cap.isOpen() function checks if the camera is open or not and returns true if the camera is open and false if the camera is not open.
While capturing the background make sure that you or your clothes don’t accidentally come into the frame.

--------------------------------------------------------------------------------------------------------------


Step 3 – Detect the cloth:

In this invisible cloak opencv project, we are using green cloth so we have to detect green color. So how can we do this?

OpenCV reads the frame as BGR colorspace. To detect any color first we have to convert the frame to HSV colorspace.

Why HSV?

HSV stands for HUE, SATURATION, and VALUE (or brightness). It is a cylindrical color space.

HUE: The hues are modeled as an angular dimension which encodes color information.
SATURATION: Saturation encodes intensity of color.
VALUE: Value represents the brightness of the color.

Explanation:

cv2.cvtColor() function converts colorspace.
Lower bound and Upper bound are the boundaries of green color.
cv2.inRange() function returns a segmented binary mask of the frame where the green color is present.

--------------------------------------------------------------------------------------------------------------

Step 4 – Apply the mask:
We have successfully detected the cloak. We want to show our previously-stored 
background in the main frame where the cloak is present. First, we need to take the only white region from the background.

Explanation:

cv2.bitwise_and() applies mask on frame in the region where mask is true (means white).

cv2.bitwise_not() inverse the mask pixel value. Where the mask is white it returns black and where is black it returns white.

--------------------------------------------------------------------------------------------------------------

Step 5 – Combine masked frames together:

Finally, we have a cloak background and current frame background. Now it’s time to combine those to get a whole frame.

Explanation:

cv2.add() adds two frames and returns a single frame.

--------------------------------------------------------------------------------------------------------------

Step 6 – Removing unnecessary noise from mask :

Explanation:

np.ones((5,5),np.uint8) create a 5×5 8 bit integer matrix.
Adjust kernel size according to your condition.
cv2.MORPH_CLOSE removes unnecessary black noise from the white region in the mask. And how much noise to remove that is defined by kernel size.
cv2.MORPH_OPEN removes unnecessary white noise from the black region.
cv2.dilate increases white region in the image.

--------------------------------------------------------------------------------------------------------------

https://machinelearningknowledge.ai/opencv-cv2-waitkey-tutorial-with-examples/


https://data-flair.training/blogs/invisible-cloak-opencv-python/
--------------
https://machinelearningknowledge.ai/make-your-own-invisibility-cloak-using-opencv-python-like-harry-potter-movie/




Look at this image, this hsv Chart of colors according to opencv2 library(in opencv2 Hue has value from 0-179, Saturation from 0-255, and value from 0-255). The x-axis represents Hue in [0,179), the y-axis1 represents Saturation in [0,255], the y-axis2 represents S = 255, while keep V = 255. To find a color, usually just look up for the range of H and S, and set v in range(20, 255).

To find the orange color, we look up for the map, and find the best range: H :[10, 25], S: [100, 255], and V: [20, 255]. So the mask is cv2.inRange(hsv,(10, 100, 20), (25, 255, 255) )
