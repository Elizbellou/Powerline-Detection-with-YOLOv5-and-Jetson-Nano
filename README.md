# Powerline Detection using a custom-trained yolov5 model deployed on Jetson Nano Dev kit
This repo contains four YOLOv5 models in .pt files, trained on an original powerline dataset with 3 object classes, i.e. towers, conductors and insulators. You can use any model as a baseline to try transfer learning on your projects related to powerline inspection tasks. 
A detailed guide on how to train-validate your own YOLO models is available in README file [here](https://github.com/Elizbellou/Tower-Insulator-Conductors-TIC-Dataset-and-Object-Detection-Models)
where you can also download our full image dataset to use with annotations (bbox and polygons).

# Performance of our YOLOv5 -based models
TABLE1. YOLOv5 performance on TESLA P100 (Colab) and YOLOv5s optimized with Tensor-RT. Input image 640X640 and NMS time per image 1-1.5ms (not included).
| PL-models | Precision | Recall | mAP@0.5 | mAP@5:95 | fps | Size |
|-----------|-----------|--------|---------|----------|-----|------|
| PL_small  | 0.81      | 0.78   | 0.82    | 0.61     | 303 |14.1MB|
| PL_medium | 0.80      | 0.78   | 0.819   | 0.597    | 119 |40.8MB|
| PL_large  | 0.788     | 0.787  | 0.817   | 0.613    | 81.9|89.3MB|
| PL_xlarge | 0.825     | 0.763  | 0.818   | 0.635    | 45.5|166MB |
|-----------|-----------|--------|---------|----------|-----|------|
|PL_small-tr| 0.817     | 0.786  | 0.823   | 0.616    | 303 |18.3MB|
| Tower     | 0.94      | 0.903  | 0.943   | 0.832    |-----|------|
| Insulator | 0.787     | 0.909  | 0.889   | 0.634    |-----|------|
|Conductors | 0.723     | 0.547  | 0.636   | 0.382    |-----|------|

TABLE 2. YOLOv5 performance on Jetson Nano (4GB) optimized with Tensor -RT.
| PL-models | Precision | Recall | mAP@0.5 | mAP@5:95 | fps on live video inference with imgsz 320 |
|-----------|-----------|--------|---------|----------|--------------------------------------------|
|PL_small-tr| 0.811     | 0.783  | 0.821   | 0.596    | 30-33                                      |
| Tower     | 0.937     | 0.935  | 0.958   | 0.825    |--------------------------------------------|
| Insulator | 0.782     | 0.89   | 0.881   | 0.599    |--------------------------------------------|
|Conductors | 0.713     | 0.525  | 0.625   | 0.364    |--------------------------------------------|

# Inference on video with Jetson Nano
Inference on drone footage using Jetson Nano dev kit can be found [here](https://youtu.be/OjKJn98CTjA)
# Impementation
## Connect Pixhawk 4 with Jetson Nano
First connect usb port of Jetson Nano to the TELEM 2 UART port of Pixhawk and run the following command (note that you may need to change USB0, baudrate number and aircraft name, according to your project):
```
mavproxy.py --master=/dev/ttyUSB0 --baudrate=57600 --aircraft MyCopter

```
Recommended Software for ground control station is Qgroundcontrol or Mission Planner.
## Export our YOLOv5s model to Tensor-RT engine file on Jetson Nano
Download our PL_small.pt from this repo and open another terminal window
```
git clone https://github.com/ultralytics/yolov5
cd yolov5
pip install -r requirements.txt coremltools onnx onnx-simplifier onnxruntime-gpu openvino-dev tensorflow  # GPU
python export.py --path/to/weights/PL_small.pt --img 640 --device 0 --simplify --include onnx
python export.py --path/to/weights/PL_small.onnx --img 640 --device 0 --include engine

```
## Run YOLO model using a USB webcam 
Open another terminal window
```
python detect.py --path/to/weights/PL_small.engine --imgsz 640 --source 0 --classes 0 1 2 --device 0 #0 is set to use gpu memory 

```
You can check your USB Camera preview and settings following this Jetsonhacks [repo](https://github.com/jetsonhacks/USB-Camera)
## Publication
For detailed insights on the drone hardware and yolo training parameters, environment etc. please read and cite : 

E. Bellou, I. Pisica and K. Banitsas, "Real-Time Object Detection on High-Voltage Powerlines Using an Unmanned Aerial Vehicle (UAV)," 2023 58th International Universities Power Engineering Conference (UPEC), Dublin, Ireland, 2023, pp. 1-6, doi: [10.1109/UPEC57427.2023.10294447](https://ieeexplore.ieee.org/abstract/document/10294447).
keywords: {Surveillance;Poles and towers;Object detection;High-voltage techniques;Inspection;Streaming media;Autonomous aerial vehicles;Unmanned Aerial Vehicles (UAVs);high-voltage powerlines;computer vision;object detection;custom dataset}

