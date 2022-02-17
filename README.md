Part of the concurrent computing for robotics course JEMARO February 2022

## Computing examples
#### Good OpenCL tutorial: https://streamhpc.com/blog/2015-03-16/how-to-install-opencl-on-windows/
#### Download CUDA from: https://developer.nvidia.com/cuda-downloads

## Cuda installation - Linux
[Source](https://linuxhandbook.com/setup-opencl-linux-docker/)

### Install the NVIDIA Container Runtime
Here, you have to additionally install the nvidia-container-runtime package.

To be able to install it, you must first add the repository details. Make sure you have Curl installed if you haven't already got it on your system.

```
sudo apt install curl
curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-container-runtime/$distribution/nvidia-container-runtime.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-runtime.list
sudo apt update
sudo apt install nvidia-container-runtime
```

### Building the Dockerfile
So now that you have the necessary Dockerfile to get started, let's build it. I'm naming the image as nvidia-opencl:

```
docker build -t nvidia-opencl .
```

### Launch the OpenCL Container
Based on the new image that you just built, it's time to launch the new OpenCL container!

First, permit your Linux username on the local machine to connect to the X windows display with the following command:

```
xhost +local:username
```

With the following command, you can now directly enter the local container's shell based on the new image just created:

```
sudo docker run --rm -it --gpus all -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$DISPLAY nvidia-opencl
```
