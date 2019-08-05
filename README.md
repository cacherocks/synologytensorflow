# TensorFlow with compiled wheel & libraries for Docker Home Assistant on Synology DS918+ 

Works with Docker Home Assistant 0.96.5 (Python 3.7.4).

## Wheel Specs:
* TensorFlow 1.14.1
* Python 3.7
* No AVX instruction set
* Only CPU
* Build on DSM 6.2.2-24922 Update 2, INTEL Celeron J3455

## Download
* Wheel: https://drive.google.com/file/d/1WmU_NGkJ4rGURgqBtQw7y5NNSVD_sxOA/view?usp=sharing
* Recommended model: http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz
* Already compiled libraries: https://drive.google.com/file/d/1jQRqsSVi2hr9G6hWGwjgyfvLMOVTHHGE/view?usp=sharing

## Install:

**1. Download object_detection.zip, unzip & copy to:**
```
/HA config dir/tensorflow/object_detection/
```
**2. Download recommended model & copy to:**
```
/HA config dir/tensorflow/faster_rcnn_inception_v2_coco_2018_01_28/
```
**3. Download wheel & copy to:**
```
/HA config dir/tensorflow/
```
**4. Create tmp folder:**
```
/HA config dir/tensorflow/tmp/
```
**5. Edit HA config:**
```
image_processing:
  - platform: tensorflow
    scan_interval: 600
    source:
      - entity_id: camera.*
      - entity_id: camera.*
      - entity_id: camera.*
      - entity_id: camera.*
    file_out:
      - "/config/tensorflow/tmp/{{ camera_entity.split('.')[1] }}_latest.jpg"
      - "/config/tensorflow/tmp/{{ camera_entity.split('.')[1] }}_{{ now().strftime('%Y%m%d_%H%M%S') }}.jpg"
    model:
      graph: /config/tensorflow/faster_rcnn_inception_v2_coco_2018_01_28/frozen_inference_graph.pb
      categories:
        - cat
        - person
        - backpack
        - umbrella
        - handbag
        - suitcase
        - bottle
        - wine glass
        - cup
        - fork
        - spoon
        - knife
        - banana
        - apple
        - sandwich
        - orange
        - broccoli
        - carrot
        - pizza
        - donut
        - cake
        - chair
        - potted plant
        - dining table
        - toilet
        - laptop
        - mouse
        - remote
        - keyboard
        - cell phone
        - microwave
        - oven
        - book
        - scissors
        - hair drier
        - toothbrush
```
**5. Install wheel inside HA docker container via terminal: **
```
docker exec -it homeassistant  /bin/bash
pip3 install /config/tensorflow/tensorflow-1.14.1-cp37-cp37m-linux_x86_64.whl
```

**6. Reboot HA**
