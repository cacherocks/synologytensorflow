# Synology DS918+ TensorFlow for Docker Home Assistant

Works with Docker Home Assistant 0.96.5 (Python 3.7.4).

## Wheel Specs:
* TensorFlow 1.14.1
* Python 3.7
* No AVX instruction set
* Only CPU

## Built on:
* DSM 6.2.2-24922 Update 2
* INTEL Celeron J3455

## Download
* Wheel: https://drive.google.com/file/d/1WmU_NGkJ4rGURgqBtQw7y5NNSVD_sxOA/view?usp=sharing
* Recommended model: http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz
* Already compiled libraries: 

Wheel install inside HA docker container: 
```
pip3 install tensorflow-1.14.1-cp37-cp37m-linux_x86_64.whl
```

My HA config:
```
image_processing:
  - platform: tensorflow
    scan_interval: 600
    source:
      - entity_id: camera.kabinet
      - entity_id: camera.koridor
      - entity_id: camera.kuhnya
      - entity_id: camera.prihozhaya
    file_out:
      - "/config/tmp/{{ camera_entity.split('.')[1] }}_latest.jpg"
      - "/config/tmp/{{ camera_entity.split('.')[1] }}_{{ now().strftime('%Y%m%d_%H%M%S') }}.jpg"
    model:
      graph: /tensorflow/faster_rcnn_inception_v2_coco_2018_01_28/frozen_inference_graph.pb
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
