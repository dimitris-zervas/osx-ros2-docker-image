# osx-ros2-docker-image

ROS 2 Docker images for OSX. The images are following the tutorials for installing ros2 on your Ubuntu machine.

[LINK](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html)

## Development setup

Those Dockerfiles were tested on:

* MacBook Pro (Intel chip)
* MacOS Ventura - Version 13.1
* Docker version 20.10.17, build 100c701

## ROS2 Desktop Install

This image follows the **full** Desktop Install (Recommended): ROS, Rviz, Gazebo, demos and tutorials.

To build the image, run the following command from a terminal that points to the root directory of this repository (where this README file is):

```bash
docker build -t ros2-osx-full ./ros2_full_desktop
```

where the `ros2-osx-full` is the tag of the image you have just built and `./ros2_full_desktop` is the folder where the _Dockerfile_ for this image is.

## ROS2 Bare Bones

This image follows the ROS-Base Install (Bare Bones): Communication libraries, message packages, command line tools. No GUI tools.

To build the image, run the following command from a terminal that points to the root directory of this repository (where this README file is):

```bash
docker build -t ros2-osx-bare-bones ./ros2_bare_bones
```
 
where the `ros2-osx-bare-bones` is the tag of the image you have just built and `./ros2_bare_bones` is the folder where the _Dockerfile_ for this image is.

## Give it a try

To make sure that the container created from the "full" image above is ready to use ros2, you can run a simple talker-listener experiment. You will need two terminals:


In the first terminal, run the following:

```bash
docker run -it --rm ros2-osx-full /bin/bash
```

The above command will create a new container out of the specified image, and start a bash terminal inside this container. In this bash terminal of the container, run the following:

```bash
ros2 run demo_nodes_py listener
```

In the second terminal, run the following:

```bash
docker run -it --rm ros2-osx-full /bin/bash
```

The above command will create a new container out of the specified image, and start a bash terminal inside this container. In this terminal of the container, run the following:

```bash
ros2 run demo_nodes_cpp talker
```

If everything was created/installed/set up properly, you should see the second container publishing messages and the first container listening to those messages.


# Next Steps

You can see how you can use Rviz2 Gazebo and ros2 here [here](./ros2_gazebo_rviz/README.md)