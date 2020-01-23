FROM bpinaya/robond-docker

#RUN apt-get update   to be fixed

RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
RUN rm /etc/apt/sources.list.d/arc*
RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install -y aptitude
RUN apt-get install -y vim
RUN apt-get install -y ros-kinetic-qt-build
RUN apt-get install -y ros-kinetic-pcl-ros
RUN apt-get install -y qt4-dev-tools
RUN apt-get install -y ros-kinetic-pcl-ros
RUN apt-get install -y ros-kinetic-qt-ros
RUN apt-get install -y ros-kinetic-opencv3
#RUN apt-get install -y ros-kinetic-opencv-apps
RUN apt-get install -y libopencv-dev
RUN git clone https://github.com/simonflueckiger/rviz-textured-quad.git /home/ubuntu/ros_ws/src/rviz-textured-quad


