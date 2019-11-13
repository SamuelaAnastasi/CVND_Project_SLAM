# CVND Project: Landmark Detection & Tracking (SLAM)

This is the final project of the Udacity's Computer Vision Nanodegree. In this project, we’ll be localizing a robot in a 2D grid world. The basis for simultaneous localization and mapping (SLAM) is to gather information from a robot’s sensors and motions over time,
and then use information about measurements and motion to re-construct a map of the world.

### 1. Robot Class

Robot motion and sensors have some uncertainty associated with them. For
example, the speedometer reading will likely overestimate or underestimate the speed of a car going up / down a hill because it cannot perfectly account for gravity. Similarly, we cannot perfectly predict the motion of a robot. A robot is likely to slightly overshoot or undershoot a target location.

In the first notebook, we’ll create a robot and move it around a 2D grid world. The sense function for this robot allows it to sense and keep track of landmarks in a given 2D grid
world, the robot’s move function will move it some distance (dx, dy).

### 2. Data

To perform SLAM, we’ll collect a series of robot sensor measurements
and motions, in that order, over a defined period of time. Then we’ll use only this data to re-
construct the map of the world with the robot and landmark locations. You can think of SLAM as
performing what we’ve done in this notebook, only backwards. Instead of defining a world and
robot and creating movement and sensor data, it will be up to you to use movement and sensor
measurements to reconstruct the world!

### 3. Omega and Xi
To implement Graph SLAM, a matrix and a vector (`omega` and `xi`, respectively) are introduced.
The matrix is square and labelled with all the robot poses (xi) and all the landmarks (Li). Every
time the robot makes an observation, for example, as it moves between two poses by some distance
dx and can relate those two positions, we can represent this as a numerical relationship in these
matrices.

### 4. Landmark Detection and Tracking
In the last notebook we’ll implement SLAM for robot that moves and senses in a 2 dimensional, grid
world! SLAM gives us a way to both localize a robot and build up a map of its environment as a
robot moves and senses in real-time. This is an active area of research in the fields of robotics
and autonomous systems. Since this localization and map-building relies on the visual sensing of
landmarks, this is a computer vision problem

We define a function, `slam`, which takes in six parameters as input and returns the vector *mu*.  *mu* contains the (x,y) coordinate locations of the robot as it moves, and the positions of landmarks that it senses in the world. The `make_data` function, generates a world grid with landmarks in it and then generates data by placing a robot in that world and moving and sensing over some number of time steps.


### 5. Implement Graph SLAM
In addition to data, the `slam` function will also take in:
* N - The number of time steps that a robot will be moving and sensing
* num_landmarks - The number of landmarks in the world
* world_size - The size (w/h) of your world
* motion_noise - The noise associated with motion; the update confidence for motion should be 1.0/motion_noise
* measurement_noise - The noise associated with measurement/sensing; the update weight for measurement should be 1.0/measurement_noise

### 5. Run SLAM and visualize the constructed world
The data that is generated is random, but we did specify the number, N, or time steps that the
robot was expected to move and the `num_landmarks` in the world which the implementation of
slam should see and estimate a position for.

The final result displays two lists:
1. Estimated poses, a list of (x, y) pairs that is exactly N in length since this is how many motions the robot has taken. The very first pose should be the center of the world, i.e. [50.000, 50.000] for a world that is 100.0 in square size.
2. Estimated landmarks, a list of landmark positions (x, y) that is exactly num_landmarks in length.

Printing out the exact landmark locations when this data was created, we should see values that are very similar to those coordinates, but not quite (since slam must account for noise in motion and measurement).

Displaying through [Seaborn](https://seaborn.pydata.org/index.html) the heatmaps for the final `omega` matrix (blu), `xi` (orange) and `mu` (green) vectors.

![Seaborn Heatmaps omega - xi - mu](https://raw.githubusercontent.com/SamuelaAnastasi/CVND_Project_SLAM/master/images/final_heatmaps.jpg)

Using the `display_world` function from the helpers.py file we can finally visualize the final position of the robot and the position of landmarks, created from only motion and measurement.

![SLAM world](https://raw.githubusercontent.com/SamuelaAnastasi/CVND_Project_SLAM/master/images/final_world.png)
