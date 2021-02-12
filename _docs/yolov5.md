# docker 
  $ docker pull ultralytics/yolov5
  $ docker run -it --rm --name yolov5 --ipc=host --gpus all -v /code:/code ultralytics/yolov5
  
# download data samples
  - https://github.com/ultralytics/yolov5/releases/download/v1.0/coco128.zip
  - organize dataset
    - {dataset name}/{images/labels}/{train|val}/{image name.jpg}
