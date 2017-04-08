# **Finding Lane Lines on the Road** 

---

[//]: # (Image References)

[pipeline]: ./pipeline.png
[crack]: ./test_images/challenge2.jpg

---

### Reflection

### 1. Pipeline structure
My pipe line includes 6 stages:

1. color selection
1. Gaussian blur
1. Canny edge detection
1. select region of interest
1. Hough line detection
1. extrapolate lines

Here is the result the output of each stages using one frame in challenge video
![alt text][pipeline]

### Some notes regarding to pipeline

1. The 2 stages contributing most in terms of filtering out irrelevant information are

    1. color selection
    1. select region of interest

Gettting good output from these 2 stages is very important. It'll make tuning other stages quite easily (such as Hough line detection parameters). On the other hand, it's very hard, if not impossible, to tune other stages if not doing well in these 2 stages.


### 2. Identify potential shortcomings with your current pipeline

1. one assumption is the line color on the road are either yellow or white. If there're other colors, color selection will fail

1. another assumption is the line fall in a range of slope (absolute slope 0.4~2). It'll ignore lines that are near flat or vertical, which can happen if sharp turn (flat) or wide track (vertical)

1. another potential problem is when traffic is heavy on the road and lines are blocked by other vehicles.

### 3. Suggest possible improvements to your pipeline

1. For the color selection problem, a possible solution is to use multiple masks and then combine them

2. The cause of a the slope problem above is in last extrapolation stage, where only lines with certain range of slope and interception are considered. This is to avoid 'crack' on the road like below.

![alt text][crack]

With good color section, the problem will be less likely but not completely to happen. Another improvement is to 'memorize' line info between frames and therefore can use choose lines close to previous frame under the assumption that line slope change is continuous.
