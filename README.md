# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining your solution. We have included template files to be used both for the [code](https://github.com/udacity/CarND-LaneLines-P1/blob/master/P1.ipynb) and the [writeup](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md).The code file is called P1.ipynb and the writeup template is writeup_template.md 

To meet specifications in the project, take a look at the requirements in the [project rubric](https://review.udacity.com/#!/rubrics/322/view)


Creating a Great Writeup
---
For this project, a great writeup should provide a detailed response to the "Reflection" section of the [project rubric](https://review.udacity.com/#!/rubrics/322/view). There are three parts to the reflection:

1. Describe the pipeline

2. Identify any shortcomings

3. Suggest possible improvements

We encourage using images in your writeup to demonstrate how your pipeline works.  

All that said, please be concise!  We're not looking for you to write a book here: just a brief description.

You're not required to use markdown for your writeup.  If you use another method please just submit a pdf of your writeup. Here is a link to a [writeup template file](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md). 


The Project
---

## If you have already installed the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) you should be good to go!   If not, you should install the starter kit to get started on this project. ##

**Step 1:** Set up the [CarND Term1 Starter Kit](https://classroom.udacity.com/nanodegrees/nd013/parts/fbf77062-5703-404e-b60c-95b78b2f3f9e/modules/83ec35ee-1e02-48a5-bdb7-d244bd47c2dc/lessons/8c82408b-a217-4d09-b81d-1bda4c6380ef/concepts/4f1870e0-3849-43e4-b670-12e6f2d4b7a7) if you haven't already.

**Step 2:** Open the code in a Jupyter Notebook

You will complete the project code in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

Jupyter is an Ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, use terminal to navigate to your project directory and then run the following command at the terminal prompt (be sure you've activated your Python 3 carnd-term1 environment as described in the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) installation instructions!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  Follow the instructions in the notebook to complete the project.  

**Step 3:** Complete the project and submit both the Ipython notebook and the project writeup

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).



## 1. Description of pipeline

The pipeline is given as follow:
(1) transform the RGB image into gray image
(2) include Gaussian smoothing with gaussian_blur function for suppressing noise and spurious gradients by averaging
(3) detect edges with canny function
(4) get the region of interest (ROI) of edges with a quadrilateral region mask
(5) use Hough transform to find lane lines in the ROI area
(6) separate line segments by their slope to decide which segments are part of the left line and which segments are part of the the right line
(7) reduce noise by get rid of horizental lines, which abs(slope) is < 0.4)
(8) fit the left lane and the right lane use np.polyfit(y,x,1) function to extrapolate to the top and bottom of the lane
(9) draw the lanes in region of interest and combine the found lanes with oringal image

![alt text][./test_images_output/original.png "original"]
![alt text][./test_images_output/gray.png "gray"]
![alt text][./test_images_output/edges.png "edges"]
![alt text][./test_images_output/edges_in_ROI.png "edges_in_ROI"]
![alt text][./test_images_output/fitting_lanes.png "fitting_lanes"]
![alt text][./test_images_output/lanes_in_ROI.png "lanes_in_ROI"]
![alt text][./test_images_output/final.png "final"]

<img src="test_images_output/original.png" width="480" alt="original" />
<img src="test_images_output/gray.png" width="480" alt="gray" />
<img src="test_images_output/edges.png" width="480" alt="edges" />
<img src="test_images_output/edges_in_ROI.png" width="480" alt="edges_in_ROI" />
<img src="test_images_output/fitting_lanes.png" width="480" alt="fitting_lanes" />
<img src="test_images_output/lanes_in_ROI.png" width="480" alt="lanes_in_ROI" />
<img src="test_images_output/final.png" width="480" alt="final" />
The test image outputs are also in "test_images_output" Folder.

## 2. Potential shortcomings

(1) the parameters for canny edges detection and the choice of region of interest and the parameters for Hough transform are depending on the car direction and road conditions. So this pipeline can only work well under this specific data.
(2) the separation of left and right is only depending on the slopes of line segements. The influence of outliers of line segements have not been eliminated.

## 3. Possible improvements
(1) realize the automatically adjustment of parameters above mentioned.
(2) get rid of outlier of line segements.
(3) apply more efficient lanes separation methods.
