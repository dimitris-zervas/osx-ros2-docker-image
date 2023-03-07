# Rviz in novnc

This documentation will guide you on how to display an x11 application running on the docker container, in your browser. The application will be `rviz2` and we will use a `novnc` docker image that will host the novnc server.


# Prerequisites

We are going to use a docker-compose file that requires the `ros2-osx-full` to be already built into your system. To check if you have this image, you can run it in a terminal:

```bash
docker images | grep ros2-osx-full
```

If you cannot find this image, you can find instructions [here](../README.md#ros2-desktop-install) on how to build it.

# Run the services

We will run two services using the `docker-compose.yaml` file:

* ros: this will run a container out of the `ros2-osx-full` image
* novnc: this will host the novnc server

Run the following from a terminal that points to the root directory of this repo

```bash
docker-compose -f ./ros2_with_rviz/docker-compose.yaml up
```

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
eb57ee93ab87   ros2-osx-full         "tail -f /dev/null"    3 seconds ago   Up 2 seconds                           ros2_with_rviz-ros-1
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


# Clean up

You can hit `ctrl-c` in the terminal you run the `docker-compose` command to stop everything.
