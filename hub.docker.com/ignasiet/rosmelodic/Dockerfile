FROM osrf/ros:melodic-desktop-full
LABEL maintainer="Ignasi Andres <ignasi@ntu.ai>"
LABEL description="A docker with a ROS configured."

# place here your application's setup specifics
# RUN rosdep init 
RUN apt-get update
RUN rosdep update
RUN echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
RUN /bin/bash -c "source ~/.bashrc"

#RUN source ~/.bashrc

RUN apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential -y
