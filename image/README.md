# Image
## basic manipulation
- `docker search ubuntu:xenial`: search all images from the remote registry
- `docker image pull <repo>:<tag>`: download an image from the remote registry to the local registry
  - `docker image pull <repo>`: if we don't specify an image tag, Docker uses latest as default tag
  - `docker image pull -a <repo>`: download all the images of the repo  
  - `docker image pull gcr.io/nigelpoulton/tu-demo:v2`: download from a third-party registry
- `docker image ls`: list all images in the local registry
  - `docker image ls -q`: display only image ID 
- `docker image inspect ubuntu:xenial`: inspect a local image
- `docker image tag old_image:old_tag new_image:new_tag`: change the tag of a local
- `docker image rm Image_ID`: remove a local image
  - `docker image rm $(docker image ls -q) -f`: delete all images on ths host

## create/commit/ push
- `docker container commit -m <comment> -a <author> CT_ID Image_Name:TAG`: create an image from an existing container
- push to a remote registry
  - `docker login`: login
  - `docker image push wukongsun/xenial:net`： upload to the remote registry 

## TP
### Download a MySQL image
- `docker image list`
- `docker search mysql`
- `docker pull mysql`
- `docker image list`
- `docker ps -a`

### Create a Xenial Image with ifconfig
- `docker container run -it --rm ubuntu:xenial /bin/bash`
- in the container, run:
  - `apt update`
  - `apt install net-tools`
- from another terminal: `docker container ps`, where you can find `CT_ID`
- `docker container commit -m "xenial with net-tools" -a "wukong" CT_ID wukongsun/xenial:net`
- `docker login`
- `docker image push wukongsun/xenial:net`
