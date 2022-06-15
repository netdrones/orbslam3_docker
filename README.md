# ORB_SLAM3 docker

This docker is based on ros melodic ubuntu 18.

There are two versions available:

- CPU based (Xorg Nouveau display)
- Nvidia Cuda based.

To check if you are running the nvidia driver, simply run `nvidia-smi` and see
if get anything.

Based on which graphic driver you are running, you should choose the proper
docker. For cuda version, you need to have [nvidia-docker
setup](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)
on your machine.

---

## Compilation and Running

Steps to compile the Orbslam3 on the sample dataset:

```sh
./download_dataset_sample.sh
# if you have just a cpu
build_container_cpu.sh
# if you have nvidia gpu
build_container_cuda.sh
```

Now you should see ORB_SLAM3 is compiling.

To run a test example:

```sh
docker exec -it orbslam3 bash
cd /ORB_SLAM3/Examples &&. /euroc_examples.sh
```

## Running on MacOS

If you have a Mac, you will find that this has no X11 connection, so you need
to based on [gist](https://gist.github.com/paul-krohn/e45f96181b1cf5e536325d1bdee6c949):

```sh
brew install xquartz
# go to Xquartz Preferences Security  allow connections from network clients
# restart xquartz
open -a xquartz
xhost +localhost

# to test if this works see if xeyes comes up
xeyes
# now test to see if docker works disable host checking
# try xeyes and exit the app to kill the container
docker run -it --rm -e DISPLAY=host.docker.internal:0 gns3/xeyes
# try firefox
docker run -it --rm -e DISPLAY=host.docker.internal:0 jess/firefox
# now run it with orbslam
docker run -it --rm -e DISPLAY=host.docker.internal:0 orbslam3 bash
cd Examples
./euroc_examples.sh

```

## Using VSCode or Sublime

You can use vscode remote development (recommended) or sublime to change codes.

- `docker exec -it orbslam3 bash`
- `subl /ORB_SLAM3`
