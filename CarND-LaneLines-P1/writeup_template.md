# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[image1]: ./test_videos_output/144_res_can.jpg "Canny Image for white color path"

[image2]: ./test_videos_output/248_res_can.jpg "Canny Image for black color path"

[imageA]: ./test_images_output/res_gblur_solidYellowLeft.jpg "Gary Scale"

[imageB]: ./test_images_output/res_canny_solidYellowLeft.jpg "Canny Model"

[imageC]: ./test_images_output/res_roi_solidYellowLeft.jpg "Region of Interest"

[imageD]: ./test_images_output/res_hough_solidYellowLeft.jpg "Hough Transformation"

[imageE]: ./test_images_output/res_solidYellowLeft.jpg "Final Output"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

I started to play around with the images first by modifying different parameters like Canny thresholds, Region Of Interest vertices and Hough transformation values.

I feel these are the main parameters which play a very important role in determining what is present in a given image.

**Canny Thresholds :** These parameters will give you a basic idea of change in gradient intensities thus providing an outline of different objects.

**Region Of Interest :** Helps us to concentrate on useful parts of the image (or area based on our goal) and reduce computation time as well.

**Hough Transformation :** Helps in detecting the sides line patterns (like solid or gap between broken lines). We can also use this find Zebra crossing and other  lane  markings

Below I stacked all the images which are being processed at each step of the algorithm.

* I did not modify any predefined functions
* I have added my own functions for lane detections for images and videos.
* created `lane_finding_pipeline` function for images
* created `process_image_video` function for videos
* I structured all the parameters that are needed in lane detection algorithms into python dictionaries and used them to pass into these functions.

```
        kernel_size = 3
        canny_val = {"low":75,"high":100}

        roi_val = {"rb": (0,590), 
                   "rt": (500,290),
                   "lt": (500,290),
                   "lb": (885,540)}

        hough_parms = {

            "rho"               : 2          ,  # distance resolution in pixels of the Hough grid
            "theta"             : np.pi/180  ,  # angular resolution in radians of the Hough grid
            "threshold"         : 80         ,  # minimum number of votes (intersections in Hough grid cell)
            "min_line_length"   : 40         ,  # minimum number of pixels making up a line
            "max_line_gap"      : 20         ,  # maximum gap in pixels between connectable line segments
        }
```

![alt text][imageA]



![alt text][imageB]



![alt text][imageC]



![alt text][imageD]



![alt text][imageE]


### 2. Identify potential shortcomings with your current pipeline

Initially I experimented a lot with these parameters individually and tried to understand how its generating the final output.

* Modifying Canny threshold values effects how object borders are determined

* Modifying Region of Interest values will not detect the lines even though other parameters are correctly applied

* Modifying Hough Transformation values will detect unnecessary objects with-in the Region Of Interest. For example if the road color changes to white, the algorithm creates       more red   lines since it cannot identify with current values and may need some more tools). The third video is the best choice to try this. 

When Road color is white

![alt text][image1]

When Road Color is black

![alt text][image2]


* If I increase the parameter values to high side, the video could only be processed for few secs which means that it couldn't find any lanes with such higher values

* If I decrease the parameter values to lower range, video is processed correctly but not upto to the mark with different road conditions.


### 3. Suggest possible improvements to your pipeline

* Modify the pipeline function such that it can take any input format and process them, this will gives to play around with multiple range of values

* I believe that using Machine Learning concepts, further down the course if we can modify the parameters on the go based on road conditions through a ML model, predict all the   above values and apply them would be a very huge step.
