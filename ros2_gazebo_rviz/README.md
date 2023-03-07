# ROS2 with Gazebo and Rviz

This documentation will guide you on how to display -in general- any x11 application running on a docker container, in your browser. More specifically, we will run two applications, the _gazebo_ simulator and `rviz2` and we will use a `novnc` docker image that will host the novnc server.

---


# Prerequisites

We are going to use a docker-compose file that requires the `ros2-osx-full` to be already built into your system. To check if you have this image, you can run it in a terminal:

```bash
docker images | grep ros2-osx-full
```

If you cannot find this image, you can find instructions [here](../README.md#ros2-desktop-install) on how to build it.

----

# Run the services

We will run three services using the `docker-compose.yaml` file:

* ros: this will run a container out of the `ros2-osx-full` image.
* gazebo: this will run a container out of the `ros2-osx-full` image.
* novnc: this will host the novnc server

Run the following from a terminal _that points to the root directory of this repo_.

```bash
docker-compose -f ./ros2_with_rviz/docker-compose.yaml up
```

---

# Validate

To make sure that everything is set up properly you can:

## novnc server

Go to your browser and open the `http://localhost:8080/vnc.html` page.

## Run rviz2 from the ros service

To run the rviz2 from the container of the `ros` service, you need to get access to a _bash_ terminal of that container. To do so, you need to first get the container ID.

```bash
docker container list
```

The output of the above command should have a line that looks like this:

```
9e9eb496a5a7   ros2-osx-full   "tail -f /dev/null"   13 seconds ago   Up 12 seconds   ros2_gazebo_rviz-ros-1
```

The `eb57ee93ab87` is the ID we are looking for. **This ID will be different for you**

The following command will give you access to a _bash_ terminal from that container:

```bash
docker exec -it eb57ee93ab87 /bin/bash
```

Now you can run the `rviz2` app:

```bash
ros2 run rviz2 rviz2
```

Go back to your browser under the `http://localhost:8080/vnc.html` URL and you should see the `rviz` up and running.


## Run Gazebo from the gazebo service

To run the rviz2 from the container of the `ros` service, you need to get access to a _bash_ terminal of that container. To do so, you need to first get the container ID.

```bash
docker container list
```

The output of the above command should have a line that looks like this:

```
bdaacf1549ee   ros2-osx-full   "tail -f /dev/null"   13 seconds ago   Up 12 seconds   ros2_gazebo_rviz-gazebo-1
```

The `bdaacf1549ee` is the ID we are looking for. **This ID will be different for you**

The following command will give you access to a _bash_ terminal from that container:

```bash
docker exec -it bdaacf1549ee /bin/bash
```

Now you can run the `gazebo` simulation:

```bash
ign gazebo -v 4 -r visualize_lidar.sdf
```

Go back to your browser under the `http://localhost:8080/vnc.html` URL and you should see the `gazebo` up and running.

Note! You can follow [this tutorial](https://docs.ros.org/en/humble/Tutorials/Advanced/Simulators/Gazebo.html#visualizing-lidar-data-in-ros-2) on how you plot the data from the `laser_scan` topic in _gazebo_, to _rviz_.

----




# Clean up

You can hit `ctrl-c` in the terminal you run the `docker-compose` command to stop everything.
