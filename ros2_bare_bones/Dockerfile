# Docs: https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#resources
FROM ubuntu:jammy

RUN apt update
RUN apt install -y curl gnupg 

# Set up locales: https://hub.docker.com/_/ubuntu - Locales section
RUN apt install -y locales
RUN rm -rf /var/lib/apt/lists/* \
	&& localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8



# Set up sources: https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#setup-sources
RUN apt update
RUN apt install -y software-properties-common
RUN add-apt-repository restricted

## Now add the ROS 2 GPG key with apt.
RUN apt update
RUN  curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

## Then add the repository to your sources list.
RUN sh -c 'echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null'


# Install ROS 2 packages: https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#install-ros-2-packages
RUN apt update
RUN apt upgrade -y

# ROS-Base Install (Bare Bones): Communication libraries, message packages, command line tools. No GUI tools.
RUN DEBIAN_FRONTEND=noninteractive apt install -y ros-humble-ros-base

# Whenever you run a new contaner with an interactive terminal,
# this command will be run to set up your ros environment.
RUN echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc

# Set up your workspace
RUN mkdir -p /home/ros2_ws/src
WORKDIR /home/ros2_ws