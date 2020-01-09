FROM cpswarm/ros-kinetic:latest

ENV HOME=/home
RUN rosdep update

RUN apt-get update -y

RUN apt-get install apt-utils git cmake g++ libfltk1.1 libfltk1.1-dev libjpeg8-dev libpng12-dev libglu1-mesa-dev libltdl-dev -y \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*

RUN echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc \
    && echo "export LD_LIBRARY_PATH=\$LD_LIBRARY_PATH:/usr/local/lib" >> ~/.bashrc

RUN mkdir $HOME/stage4
WORKDIR  $HOME/stage4
RUN git clone --single-branch --branch cpswarm git://github.com/robotnikautomation/Stage.git
WORKDIR  $HOME/stage4/Stage
RUN mkdir build
WORKDIR  $HOME/stage4/Stage/build
RUN cmake ..
RUN make
RUN make install
