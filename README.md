This file makes use of your webcam please make your permission is granted 


I have included hsv_value_adjust.py 


To find out HSV values for any given color execute hsv_value_adjust.py and bring an object of the color in front of camera.
Adjust values till only the color you want is visible 
Include HSV min,max values to the "mycolors" list.


Keep in mind that HSV values may differ w.r.t lighting conditions.


Color tracing is simple
1) First we convert BGR to HSV
2) Get contours for each frame of your webcam 
3) Then draw each point as it is recognized

One issue I did face was that the program recognised my clothes as well whereas I wanted objects such as pens to be recognized.


To solve this I made the area under consideration only to be less than 250, i.e, only objects with area less than 250 will be considered

Output:

![alt text]https://github.com/siddhantripathi/Projects-OpenCV/blob/main/Screenshot%202021-02-02%20123332.PNG.jpg
