# ImageProcessing_PhaseOne
First stage, we wanted to apply hough transform which we studied using opencv_python..
  A) 1st script is Line_detection.ipynb which take  lines.jpg as input image ,transform it to gray scale to be easy to be processed then applying hough transform to the hough space to detect line.
     
 
  B)  2nd script is line_detection_video.ipynb which takes road_car_view.mp4 frames to be process with hough transform then the output video is displayed when the script is executed only..
     

Functions:
cv2.cvtColor(img, cv2.COLOR_BGR2GRAY): which take the image to transform it to gray_scale one.
cv2.HoughLinesP(edges, 1, np.pi/180, 50): which transforms the image to hough space with certain resolution to be processed to detect lines.
     
   


2. Second stage, we use Laning_Script.ipynb  to detect lane pixels and fit to find the lane boundery and to determine the curvature of the lane and vehicle position with respect to center.
  Steps:-

After using camera calibration algorithm by executing the camera_calibration.py to compute the camera calibration matrix and distortion coefficients camera_calib.p.
Apply undistortion algorithm according to the coefficients we got in camera_calibration step by using open_cv cv2.undistort(img,mtx,dist,None,mtx) to remove the effect of lens distortion .
          
 
   iii. Detecting edges using color transforms, gradients and other methods, one of the important methods is sobel filter which gets the image gradient in x and y....First, define sobal filter function to take the input image and the range of pixels (def abs_sobel_thresh(img, orient='x', thresh_min=0, thresh_max=255)) applying the derivative(gradient) in x and y(cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=sobel_kernel) & cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=sobel_kernel)) axis then apply proper thershold and color thershold, then transform to the binary image 8_bit.
      
 
   iv. Apply a perspective transform to rectify binary image ("birds-eye view") by using perspective_transform.p weights.
      
 
   iiv. Find lane pixels and fit with a 2nd order polynomial
      
 
    iiv. Calculate the redius of curvature using the equation besed on https://www.intmath.com/applications-differentiation/8-radius-curvature.php :
    
      curve_radius = ((1 + (2*fit[0]*y_0*y_meters_per_pixel + fit[1])**2)**1.5) / np.absolute(2*fit[0])
      
      The position of the vehicle with respect to the center of the lane is calculated with the following:
      
      
      lane_center_position = (r_fit_x_int + l_fit_x_int) /2
      center_dist = (car_position - lane_center_position) * x_meters_per_pix
      
      
      
      
    vv. Displaying the result images and video in output_images for each step and output_videos .




