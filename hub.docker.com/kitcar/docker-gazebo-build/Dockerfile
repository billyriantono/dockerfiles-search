FROM kitcar/docker-ros-build:melodic_clang_7
LABEL name=docker-gazebo-build version=melodic-gazebo9

ENV KITCAR_REPO_PATH=/
ENV CAR_NAME=dr_drift

RUN apt-get update && apt-get install -y \
ros-melodic-gazebo-ros-control ros-melodic-gazebo-ros-pkgs \
python3 gazebo9 libgazebo9-dev python-opencv python3-pip \
libgirepository1.0-dev gcc libcairo2-dev pkg-config python3-dev gir1.2-gtk-3.0

RUN apt upgrade libignition-math2 -y 

RUN apt-get update && apt-get install -y \
dbus dbus-x11 libasound2 libasound2-plugins alsa-utils \
alsa-oss pulseaudio pulseaudio-utils 

#Needed to run gazebo
RUN apt-get update && apt-get install xvfb -y

ENV DISPLAY=:1.0

# So that dbus-daemon can create /var/run/dbus/system_bus_socket
RUN mkdir /var/run/dbus

COPY [ "start_script.sh", "/"]

RUN echo "source /opt/ros/melodic/setup.bash --extend" > /root/.bashrc

