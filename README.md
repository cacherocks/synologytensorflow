# Synology DS918+ TensorFlow Wheel

Works with Docker Home Assistant 0.96.5 (Python 3.7.4).

## Wheel Specs:
* TensorFlow 1.14.1
* Python 3.7
* No AVX instruction set

## Built on:
* DSM 6.2.2-24922 Update 2
* INTEL Celeron J3455

## Download
* Wheel: https://drive.google.com/file/d/1WmU_NGkJ4rGURgqBtQw7y5NNSVD_sxOA/view?usp=sharing
* Recommended model: http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz

Install inside HA docker container: 
```
pip3 install tensorflow-1.14.1-cp37-cp37m-linux_x86_64.whl
```
