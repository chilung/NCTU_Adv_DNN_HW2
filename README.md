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

train
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/yolov4.conv.137 -map

resume train
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/backup/yolo-obj_xxxx.weights -map

train with remote server without GUI
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/yolov4.conv.137 -dont_show -mjpeg_port 8090 -map
then open URL http://ip-address:8090 

train with multiple GPU
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj-200000.cfg ./build/darknet/x64//backup/yolo-obj-200000_1000.weights -gpus 0,1 -dont_show -mjpeg_port 8090 -map

