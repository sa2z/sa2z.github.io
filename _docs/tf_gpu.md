# docker
  - self make : consider version table of tf,cuda,cudnn - https://www.tensorflow.org/install/source?hl=ko
  - maded docker - https://www.tensorflow.org/install/docker?hl=ko
    - $ docker pull tensorflow/tensorflow                     # latest stable release
    - $ docker pull tensorflow/tensorflow:devel-gpu           # nightly dev release w/ GPU support
    - $ docker pull tensorflow/tensorflow:latest-gpu-jupyter  # latest release w/ GPU support and Jupyter
    
# run docker
  $ docker run --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=6,7 -it --rm --name tf_robot --net=host -p 8890:8888 -v /code:/code tensorflow/tensorflow:latest-gpu-jupyter 
  $ docker run --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=6,7 -it --rm --name tf_robot --net=host -p 8890:8888 -v /code:/code tensorflow/tensorflow:devel-gpu  
  
# open jupyter 
  $ jupyter lab --ip 0.0.0.0 --allow-root
