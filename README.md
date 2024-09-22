# Powerline-Detection
This repo contains four YOLOv5 models in .pt form, trained on a powerline dataset with 3 object classes, i.e. towers, conductors and insulators. You can use any model as a baseline to try transfer learning on your projects related to powerline inspection tasks. 
A detailed guide on how to reproduce this project is available in README file [here](https://github.com/Elizbellou/Tower-Insulator-Conductors-TIC-Dataset-and-Object-Detection-Models)
where you can also download the full imagedataset with annotations (bbox and polygons).


TABLE1. YOLOv5 performance on TESLA P100 (Colab) and YOLOv5s optimized with Tensor-RT. Input image 640X640 and NMS time per image 1-1.5ms (not included).
| PL-models | Precision | Recall | mAP@0.5 | mAP@5:95 | fps | Size |
|-----------|-----------|--------|---------|----------|-----|------|
| Yolov5s   | 0.81      | 0.78   | 0.82    | 0.61     | 303 |14.1MB|
| Yolov5m   | 0.80      | 0.78   | 0.819   | 0.597    | 119 |40.8MB|
| Yolov5l   | 0.788     | 0.787  | 0.817   | 0.613    | 81.9|89.3MB|
| Yolov5x   | 0.825     | 0.763  | 0.818   | 0.635    | 45.5|166MB |
|-----------|-----------|--------|---------|----------|-----|------|
|Yolov5s-trt| 0.817     | 0.786  | 0.823   | 0.616    | 303 |18.3MB|
| Tower     | 0.94      | 0.903  | 0.943   | 0.832    |-----|------|
| Insulator | 0.787     | 0.909  | 0.889   | 0.634    |-----|------|
|Conductors | 0.723     | 0.547  | 0.636   | 0.382    |-----|------|

TABLE 2. YOLOv5 performance on Jetson Nano (4GB) optimized with Tensor -RT.
| PL-models | Precision | Recall | mAP@0.5 | mAP@5:95 | fps on video inference |
|-----------|-----------|--------|---------|----------|------------------------|
|Yolov5s-trt| 0.811     | 0.783  | 0.821   | 0.596    | 33                     |
| Tower     | 0.937     | 0.935  | 0.958   | 0.825    |------------------------|
| Insulator | 0.782     | 0.89   | 0.881   | 0.599    |------------------------|
|Conductors | 0.713     | 0.525  | 0.625   | 0.364    |------------------------|

Inference on drone footage using Jetson Nano dev kit can be found [here](https://youtu.be/OjKJn98CTjA)

For detailed insights please read and cite : 

E. Bellou, I. Pisica and K. Banitsas, "Real-Time Object Detection on High-Voltage Powerlines Using an Unmanned Aerial Vehicle (UAV)," 2023 58th International Universities Power Engineering Conference (UPEC), Dublin, Ireland, 2023, pp. 1-6, doi: [10.1109/UPEC57427.2023.10294447](https://ieeexplore.ieee.org/abstract/document/10294447).
keywords: {Surveillance;Poles and towers;Object detection;High-voltage techniques;Inspection;Streaming media;Autonomous aerial vehicles;Unmanned Aerial Vehicles (UAVs);high-voltage powerlines;computer vision;object detection;custom dataset}

