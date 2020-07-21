---
title: Docker Usage
category: Docker
order: 1
published: true
---

## Make docker images as a file

```
# Save as a file
    $ docker save {option} {image:tag} -o {file_name}  // --output, -o : assign file name of output
    $ docker save -o {file_name}.tar

# Load file to docker images layer // --input -i : target input_file
    $ docker load {option}
    $ docker load -i {file_name}.tar

# docker export ( docker container -> tar )
    $ docker export {container name/id} > {file_name}.tar

# docker import ( tar -> docker image)
    $ docker import {file/url}
```

|cmd|source|output|target|
|:---:|:---|:---|:---|
|'save'| container |.tar | container file system | 
|'load' |.tar| docker image (layer)| flat file system |
|'export'| container | docker image (include history) |.tar |
|'import' |.tar| docker image (include history) |docker image (layer) |


# Install Docker 
    ```
    $ sudo apt-get update
    $ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
    
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    
    $ sudo apt-key fingerprint 0EBFCD88
    
    $ sudo add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"
    
    $ sudo apt-get update
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io
    
    # assign docker command permission to other users 
    $ sudo chmod 666 /var/run/docker.sock
    
    # test
    [cpu]$ docker run hello-world
    $ docker run --gpus all nvidia/cuda:10.0-base nvidia-smi
    
    # [error] could not select device driver "" with capabilities:[[gpu]]
    $ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
    $ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
    $ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
    $ apt-get update
    $ sudo apt-get install -y nvidia-container-toolkit
    $ sudo systemctl restart docker
    
    
    ```
    
# Check docker network
    [bridges]$ docker network ls
    # create network bridge
    $ docker network create {bridge_name} --driver bridge
    # connect to bridge network
    $ docker network connect {bridge_name} {container_name}
    []$ ifconfig> docker0
    [inspect]$ docker network inspect bridge, $ docker inspect {container_name} |  jq -r  ' [0].NetworkSettings.IPAddress'
    
