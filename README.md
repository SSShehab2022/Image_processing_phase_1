# ImageProcessing_PhaseOne
## First stage
 we wanted to apply hough transform which we studied using opencv_python.
 1. 1st script is **Line_detection.ipynb** which take  **lines.jpg** as input image ,transform it to gray scale to be easy to be processed then **applying hough transform** to the     hough space to detect line.
 2. 2nd script is **line_detection_video.ipynb** which takes **road_car_view.mp4 frames**(for example) to be process with hough transform then the output video is displayed when the script is executed only..
     

#### Functions:
- **cv2.cvtColor(img, cv2.COLOR_BGR2GRAY):** which take the image to transform it to gray_scale one.
- **cv2.HoughLinesP(edges, 1, np.pi/180, 50):** which transforms the image to hough space with certain resolution to be processed to detect lines.
     
   

## Second stage
we use **Laning_Script.ipynb**  to detect lane pixels and fit to find the lane boundery and to determine the curvature of the lane and vehicle position with respect to center.


#### **Pipelining algorithm:-**

1. After using camera calibration algorithm by executing the **camera_calibration.py** to compute the camera calibration matrix and distortion coefficients **camera_calib.p**.

2. Apply undistortion algorithm according to the coefficients we got in camera_calibration step by using open_cv **cv2.undistort(img,mtx,dist,None,mtx)** to remove the effect of lens distortion.

3. Transform the image to HLS space to **consider the sunlight** as it's one of the noises(issues) we face and store saturation(s) channel which give good results with function used by opencv **cv2.cvtColor(undist_images[ii], cv2.COLOR_RGB2HLS)**.

4. Apply **sobel filter(gradient)** in **x[cv2.Sobel(gray, cv2.CV_64F, 1, 0)]** and **y[cv2.Sobel(gray, cv2.CV_64F, 0, 1)]** direction , then apply certain threshold to enchance the image edges more.

5.  Apply a **perspective transform** to rectify binary image (see the road from the top view) and use **perspective_transform.p** which is created by pre-excuted script **perspective_tranform.py** to get the **transformation matrix M** which give the perspectived image if we multiplied it to the original image matrix ,then use opencv function **cv2.warpPerspective(color_thresh_binary[idx], M, img_size)**.
      
6. Find lane pixels and fit with a **2nd order polynomial**:
   ```diff
   F(y) = A*y^2 +B*y +C for right and left road lane.
   ```
      
7. Calculate the redius of curvature using the equation besed on [https://www.intmath.com/applications-differentiation/8-radius-curvature.php]:
    ```diff
       curve_radius = ((1 + (2*fit[0]*y_0*y_meters_per_pixel + fit[1])**2)**1.5) / np.absolute(2*fit[0])
     ``` 
8. The position of the vehicle with respect to the center of the lane is calculated with the following:
     ```diff
       lane_center_position = (r_fit_x_int + l_fit_x_int) /2
       center_dist = (car_position - lane_center_position) * x_meters_per_pix
      ``` 
      




