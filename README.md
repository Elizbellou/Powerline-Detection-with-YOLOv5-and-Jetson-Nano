# Powerline-Detection
This repo contains four YOLOv5 models in .pt form, trained on a powerline dataset with 3 object classes, i.e. towers, conductors and insulators. You can use any model as a baseline to try transfer learning on your projects related to powerline inspection tasks. 


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


For detailed insights please read and cite : 

Bellou, E., Pisica, I., & Banitsas, K. (2023, August). Real-time object detection on high-voltage powerlines using an Unmanned Aerial Vehicle (UAV). In 2023 58th International Universities Power Engineering Conference (UPEC) (pp. 1-6). IEEE.
