# Defect-image-recognition-system
Deliver a vision detection system to detect the defect, and communicate with Robot by MC protocol(MELSEC Communication Protocol) for auto-remove function.

## The development consists four different stages
* Phase 1. Web camera setup: adding one additional camera to observe the defect
* Phase 2. PC server setup & PLC network module installation: PC-PLC connection
* Phase 3. Data collection: collect the image for detection system module training
* Phase 4. Robot new path design & implement new program/debug
* Phase 5. GUI design for image recognition system
![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown.](Procedure.jpg)

Experiment objective is to collect the data to train deep learning model for online monitoring and auto-classification. 
The data collection will use the webcam setup online. After PC-PLC connection complete by MC protocol, will design new path for robot to do automation.

### Neuro-network selection and evaluation
* Tensorflow model
* YOLOV5<br>
![](https://github.com/a23444452/Defect-image-recognition-system/blob/main/model%20selection.jpg)

### Training pipelines
* Folders
* Naming
![](https://github.com/a23444452/Defect-image-recognition-system/blob/main/Training%20pipelines.JPG)

### Image acquisition
* Image acquisition from video clips<br>
![](https://github.com/a23444452/Defect-image-recognition-system/blob/main/Image%20acquisition.jpg)

### Image augmentation
* Tensorflow: Keras => ImageDataGenerator<br>
  https://www.analyticsvidhya.com/blog/2020/08/image-augmentation-on-the-fly-using-keras-imagedatagenerator/
  https://www.tensorflow.org/api_docs/python/tf/keras/preprocessing/image/ImageDataGenerator
![](https://github.com/a23444452/Defect-image-recognition-system/blob/main/Tensorflow%20YOLO%20image%20augmentation.png.jpg)
* YOLO:<br>
![](https://github.com/a23444452/Defect-image-recognition-system/blob/main/Image%20augmentation%20example.jpg)

### Training & validation & learning rate
* Rescale: 1/255<br>
  – Image pixel value 0-255 => 0-1, reduce computing<br>
* Target size: training and prediction image size<br>
  – Need to be equal length and width (SPP-NET; spatial pyramid pooling)<br>
  – Found 128*128 is most suitable<br>
  – Affect performance (larger image take longer time to predict)<br>
* Batch size:<br>
  – Neuro network playground
* Class mode:<br>
  – Binary & categorical<br>

Tensorflow:<br>
![](https://github.com/a23444452/Defect-image-recognition-system/blob/main/Tensorflow_dataset.jpg)
YOLO:<br>
![](https://github.com/a23444452/Defect-image-recognition-system/blob/main/YOLO_dataset.jpg)

### PC to PLC communication through MC protocol
```
import pymcprotocol
PLC = pymcprotocol.Type3E()#If you use Q series PLC
PLC.setaccessopt(commtype="ascii")
PLC.connect(“PLC IP", PLC PORT)
```
https://pypi.org/project/pymcprotocol/
![](https://github.com/a23444452/Defect-image-recognition-system/blob/main/PLC%20setting.jpg)


