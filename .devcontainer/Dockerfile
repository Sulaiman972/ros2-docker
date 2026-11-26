FROM ros:jazzy
ARG USERNAME=USERNAME
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Delete user if it exists in container (e.g Ubuntu Noble: ubuntu)
RUN if id -u $USER_UID ; then userdel `id -un $USER_UID` ; fi

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python3-pip

# Set locale
RUN apt update 
RUN apt install locales -y
RUN locale-gen en_US en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
RUN export LANG=en_US.UTF-8

# Install ROS2 & Gazebo packages
RUN apt update && apt upgrade -y 
RUN apt install ros-jazzy-desktop ros-jazzy-ros-base -y \
    && apt install ros-jazzy-rviz2 ros-jazzy-turtle-tf2-py ros-jazzy-tf2-ros ros-jazzy-tf2-tools -y \
    && apt-get install ros-jazzy-ros-gz -y \
    && apt install ros-jazzy-gz-launch-vendor ros-jazzy-gz-tools-vendor -y

ENV SHELL /bin/bash


USER $USERNAME
CMD ["/bin/bash"]
