## Compile the darknet executable
Follow original Yolo v4 [github](https://github.com/AlexeyAB/darknet.git) README.md to make ./darknet
## test
1. Download the pretrained darknet weights. You can use this pretrained weights [here](https://drive.google.com/file/d/1lDDQ_JJmW0hv4SNGkcT1yiWcPxf459Us/view?usp=sharing)
2. Put the pretrained weights into the directory of ./build/darknet/x64/backup/
3. download the test dataset from the link [here](https://drive.google.com/file/d/1nswVLQSGupsRympzb3tUv3L94d7ADPmi/view?usp=sharing)
4. unzip the dataset into the directory of ./build/darknet/x64/data
5. perform inference
80 classes

<pre><code>./darknet detector test ./cfg/coco.data ./cfg/yolov4.cfg ./weights/yolov4.weights -ext_output ./data/dog.jpg
</code></pre>

10 digits classes

<pre><code>./darknet detector test ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/backup/yolo-obj_mAP_93.6.weights -dont_show -ext_output -out result.json < ./build/darknet/x64/data/valid.txt
</code></pre>

## train
1. Download the Yolo v4 pretrained model from [Yolov4.conv.137](https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137) and put into the directory of ./build/darknet/x64/
2. Download the train dataset from [here](https://drive.google.com/file/d/1UheRzvFHMCC2vWt5f9PTHMniRP6K_uug/view?usp=sharing). Unzip into the directory of ./build/darknet/x64/data/obj
3. open the notebook of hw_work/h5-2-label_file.ipynb to process the h5 label and come out the label file for Yolo v4 format, e.g 1.txt for 1.png. Put these label txt file in the same directory as train dataset.
<pre><code>for each object in new line:
<object-class> <x_center> <y_center> <width> <height>
Where:
<object-class> - integer object number from 0 to (classes-1)
<x_center> <y_center> <width> <height> - float values relative to width and height of image, it can be equal from (0.0 to 1.0]. For example: <x> = <absolute_x> / <image_width> or <height> = <absolute_height> / <image_height>. attention: <x_center> <y_center> - are center of rectangle (are not top-left corner).
</code></pre>
  
  
  
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/yolov4.conv.137 -map

resume train
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/backup/yolo-obj_xxxx.weights -map

train with remote server without GUI
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/yolov4.conv.137 -dont_show -mjpeg_port 8090 -map
then open URL http://ip-address:8090 

train with multiple GPU
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj-200000.cfg ./build/darknet/x64//backup/yolo-obj-200000_1000.weights -gpus 0,1 -dont_show -mjpeg_port 8090 -map

