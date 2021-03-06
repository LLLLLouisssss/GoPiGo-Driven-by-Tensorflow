# GoPiGo Driven by Tensorflow
## Intro
This readme file tends to teach you how to use [GoPiGo](http://www.dexterindustries.com/gopigo/)'s camera to record the image data and label data. And then you can use those data to train your CNN using Tensorflow. The server.py file in this repository is programmed to use your trained CNN to control your GoPiGo robot to do a simple and low level autonomous driving. [Youtube video here to see an example](https://www.youtube.com/watch?v=u7KKhGDDrEo) ```Some path in the py files might need to be changed according to your preference.```

![alt tag](http://32414320wji53mwwch1u68ce.wpengine.netdna-cdn.com/wp-content/uploads/2014/07/GoPiGo-with-Servo-and-Ultrasonic-facing-right-800x800.jpg)

### What the server.py code does:

1. create socket and listening. 

2. Build the trained network using .pb file and txt file.

3. run the network and output a label with either 'w' for go front, 'a' for go left, 'd' for turn right.

4. Send the output label to the client (GoPiGo) through TCP connection.

### What the client.py code does:

1. Capture an image in front and save it as jpg file. 

2. connect to the socket.

3. Send image to server.

4. Receive output command from server through TCP.

5. excute command to control the robot.



## Prerequisite on PC or laptop:
[Tensorflow](https://www.tensorflow.org/)

## Prerequisite on GoPiGo:
[Raspberry Pi Camera enabled](https://thepihut.com/blogs/raspberry-pi-tutorials/16021420-how-to-install-use-the-raspberry-pi-camera)

GoPiGo package installed

[vnc](https://www.raspberrypi.org/documentation/remote-access/vnc/)

## How to collect your own data




### Steps:
1.remote connect your GoPiGo through ssh
```
ssh USERNAME@IP.ADDRESS
```

2.Start remote desktop control
```
tightvncserver
vncserver :1 -geometry 1920x1080 -depth 24
```
start Remote Desktop Viewer on your PC. Then login your GoPiGo.

3. Open a terminal using your Remote Desktop Viewer on GoPiGo
4. create a folder called ```Data```, and three subfolders called ```a, w, d``` respectively.
5. run ```python datacollection.py```
6. Control your GoPiGo to follow the "road" you've built using either white paper or other materials.
7. The images will be saved in ```a, w, d``` folders. 
8. Copy or scp your ```Data``` folder to PC or Laptop and trained them by following @petewarden  [Tensorflow for Poets](https://petewarden.com/2016/02/28/tensorflow-for-poets/)

## How to control GoPiGo using your trained CNN?
1.Run server.py on laptop or desktop with wifi by typing:
```
python server.py --model=LOCATION of YOUR .pb FILE --labels=LOCATION of YOUR .txt LABEL FILE
```   

2.Run client.py on GoPiGo:
```
python client.py
```

3.You should be able to see your GoPiGo drive itself. The larger your training data set is, the better its performance will be. So collect as more data as you can !!! 

## Tips
1. When you collect data, it's faster to turn the camera of the GoPiGo to the left and label the corresponding images as 'right' or 'd'. Vice versa for the 'left' or 'a'. This requires some revise of the saving folders in the datacollection.py file.  


