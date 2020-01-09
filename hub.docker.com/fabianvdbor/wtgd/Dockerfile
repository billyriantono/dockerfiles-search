FROM ros:lunar

RUN apt-get update && \
    apt-get install -y curl libunwind8 gettext apt-transport-https apt-utils && \
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg && \
    mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg && \
    sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-xenial-prod xenial main" > /etc/apt/sources.list.d/dotnetdev.list' && \
    apt-get update && \
    apt-get install -y dotnet-sdk-2.0.2

RUN apt-get update && apt-get install -y python-pip

RUN apt-get update && apt-get install -y ros-lunar-rosserial-python \
  ros-lunar-catkin \
  ros-lunar-rosbridge-server

RUN apt-get update && apt-get install -y ros-kinetic-rosserial \
  ros-kinetic-rosserial-arduino \
  ros-kinetic-rosapi \
  ros-kinetic-desktop-full \
  ros-kinetic-joystick-drivers \
  ros-kinetic-rosbridge-server \
  ros-kinetic-rosserial-python \
  ros-kinetic-move-base \
  ros-kinetic-hector-mapping \
  ros-kinetic-ecto-opencv \
  ros-kinetic-ecto-openni \
  ros-kinetic-rosserial-server \
  ros-kinetic-teleop-twist-joy \
  ros-kinetic-teleop-twist-keyboard

  RUN apt-get update && apt-get install -y ros-lunar-rviz \
    ros-lunar-rosbash \
    ros-lunar-rqt \
    ros-lunar-rqt-tf-tree \ 
    ros-lunar-pcl-conversions \
    ros-lunar-pcl-ros \
    ros-lunar-cv-bridge \
    ros-lunar-vision-opencv

CMD [ "roslaunch" ]
