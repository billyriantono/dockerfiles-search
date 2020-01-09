# sudo docker build -t mep-vnc .
# sudo docker run -v ${PWD}/mep-master-ros2:/root/Desktop/mep-master-ros2 -it --rm -p 6080:80 mep-vnc -e GIT_NAME='Darko Lukic' -e GIT_EMAIL='lukicdarkoo@gmail.com'

FROM dorowu/ubuntu-desktop-lxde-vnc

RUN apt-get update \
	&& apt install -y iputils-ping curl git vim

# ROS1 & ROS2 repos
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' \
	&& sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116 \
	&& curl http://repo.ros2.org/repos.key | sudo apt-key add - \
	&& sh -c 'echo "deb [arch=amd64,arm64] http://repo.ros2.org/ubuntu/main xenial main" > /etc/apt/sources.list.d/ros2-latest.list'

# ROS1 & ROS2 installation
RUN apt-get update \
	&& apt install -y iputils-ping \
	&& apt install -y ros-kinetic-desktop-full \
	&& apt install -y ros-ardent-ros1-bridge ros-ardent-ament-tools ros-ardent-turtlebot2-*

RUN echo "source /opt/ros/ardent/setup.bash" > /root/.bashrc \
	&& echo 'git config --global user.email ${GIT_EMAIL}' >> /root/.bashrc \
	&& echo 'git config --global user.name "${GIT_NAME}"' >> /root/.bashrc \
	&& alias ll='ls -lah'


