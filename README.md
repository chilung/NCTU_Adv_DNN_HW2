## Compile the darknet executable
Follow original Yolo v4 [github](https://github.com/AlexeyAB/darknet.git) README.md to make ./darknet
## test
./darknet detector test ./cfg/coco.data ./cfg/yolov4.cfg ./weights/yolov4.weights -ext_output ./data/dog.jpg
./darknet detector test ./build/darknet/x64/data/obj.data ./cfg/yolo-obj-200000.cfg ./build/darknet/x64/backup/yolo-obj-200000_mAP_92.6.weights -dont_show -ext_output -out result.json < ./build/darknet/x64/data/valid.txt

train
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/yolov4.conv.137 -map

resume train
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/backup/yolo-obj_xxxx.weights -map

train with remote server without GUI
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj.cfg ./build/darknet/x64/yolov4.conv.137 -dont_show -mjpeg_port 8090 -map
then open URL http://ip-address:8090 

train with multiple GPU
./darknet detector train ./build/darknet/x64/data/obj.data ./cfg/yolo-obj-200000.cfg ./build/darknet/x64//backup/yolo-obj-200000_1000.weights -gpus 0,1 -dont_show -mjpeg_port 8090 -map

