### Darknet V4 on cuda10.1-cudnn7
- Based on [AlexeyAB YoloV3](http://https://github.com/AlexeyAB/darknet "AlexeyAB YoloV3")

### Working Environment 
- Cuda: 10.1
- Cudnn: 7
- OpenCV: 3.4.8
- Cmake: 3.16.3
- Python: 3.7  with pillow, opencv-python, pandas, numpy

### Training data
- Based on [WIDERFACE](http://shuoyang1213.me/WIDERFACE/)

### Usage 
**Get Started !**

``` sh
 docker build -t darknet .

 # mount the Docker  container
 docker run -it --gpus -v $PWD:/app/ all darknet /bin/bash 

```

Create a directory in darknet for training your model.
``` sh
mkdir Face_detection
cd Face_detection
```

Create a cfg directory inside the **Face_detection** directory.
``` sh
mkdir cfg
```

Download the training and validation data from [WIDERFACE](http://shuoyang1213.me/WIDERFACE/). Then convert the downloaded data to Yolo format by using the **convertor.py** inside the *Face_detection* directory.

Prepare the **face.data** and **face.names** for classes and labelling.

Copy **yolov4-tiny-obj.cfg** and **yolov4-tiny.conv.29** from *darknet/cfg* to *darknet/Face_detection/cfg* .

Then, modify the copied **yolov4-tiny-obj.cfg**.
```sh
batch=16
max_batches=6000
steps=4800, 5400
```

**Start the training !**
```sh
./darknet detector train ./darknet/Face_detection/cfg/face.data ./darknet/Face_detection/cfg/yolov4-tiny-obj.cfg ./darknet/Face_detection/cfg/yolov4-tiny.conv.29 -dont_show
```

Move the **weights** to *Face_detection/cfg/weights* .

Now, you can run Yolo with your web camera.

```sh
/darknet detector demo ../darknet/Face_detection/cfg/face.data ../darknet/Face_detection/cfg/yolov4-tiny-obj.cfg ../darknet/Face_detection/cfg/weights/yolov4-tiny-obj_final.weights
```
