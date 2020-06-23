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
