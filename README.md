# Social-Distance-Detection-using-OpenCV

COVID-19 outbreak has created a lot of tension and misery to many families across the globe. During this pandemic, people are adviced to not be in close contact with others to reduce the spread of the disease. But there are still many humans who are negligent about this disease by not maintaining social distance. So, I developed this project to monitor if people are maintaining social distance or not. This can help the Government monitor areas where social distancing is not practiced and enforce stricter laws.

Webcam is used to capture the video and detect people in real-time. If people are very close to each other, a red bounding box is displayed around them indicating that they are not maintainting social distance. 
<br />
<br />

![](demo.gif)


## Set Up

To begin with, use the requirements.txt file to install the dependencies.
```
pip install -r requirements.txt
```

## Execute

Use the following command to execute the code.
```
python social_distance_detection.py --prototxt SSD_MobileNet_prototxt.txt --model SSD_MobileNet.caffemodel --labels class_labels.txt
```

## Model

The MobileNet SSD model can detect 20 objects. The list of objects that can be detected can be found in the [class_labels.txt](class_labels.txt) file.
You can also load any pre-trained model from Deep Learning frameworks like Caffe, Tensorflow, Torch and Darknet. 


## Method

Single Shot object Detection (SSD) using MobileNet and OpenCV were used to detect people. A bounding box is displayed around every person detected. 

To detect the distance of people from camera, triangle similarity technique was used. Let us assume that a person is at a distance D (in centimetres) from camera and the person's actual height is H (I have assumed that the average height of humans in 165 centimetres). Using the object detection code above, we can identify the pixcel height P of the person using the bounding box coordinates. Using these values, the focal length of the camera can be calculated using the below formula:

```
Eq 1: F = (P x D) / H
```
After calculating the focal length of the camera, we can use the actual height H of the person, pixcel height P of the person and focal length of camera F to calculate the distance of the person from camera. Distance from camera can be calculated using:

```
Eq 2: D' = (H x F) / P
```
Now that we know the depth of the person from camera, we can move on to calculate the distance between two people in a video. There can be n number of people detected in a video. So the Euclidean distance is calculated between the mid-point of the bounding boxes of all the people detected. By doing this, we have got our x and y values. These pixcel values are converted into centimetres using Eq 2.

We have the x, y and z (distance of the person from camera) coordinates for every person in cms. The Euclidean distance between every person detected is calculated using the (x, y, z) cordinates. If the distance between two people is less than 2 metres or 200 centimetres, a red bounding box is displayed around them indicating that they are not maintaining social distance. The object's distance from camera was converted to feet for visualization purpose. 

## Improvements

* Various object detection models like YOLO, Faster R-CNN can be used to improve the performance and accuracy of object detection.
* Video can be calibrated to get bird's eye view for more accurate distance estimation between objects.


## References

[DNN_Object_Detection](https://github.com/TheNsBhasin/DNN_Object_Detection)

[Find distance from camera to object/marker using Python and OpenCV](https://www.pyimagesearch.com/2015/01/19/find-distance-camera-objectmarker-using-python-opencv/)
