FROM ubuntu:latest
LABEL maintainer="ugo.pattacini@iit.it"

# Non-interactive installation mode
ENV DEBIAN_FRONTEND=noninteractive

# Update apt database
RUN apt update

# Install essentials
RUN apt install -y apt-utils software-properties-common apt-transport-https sudo \
    psmisc lsb-release tmux nano wget curl telnet build-essential gdb git gitk \
    libedit-dev libxml2-dev autoconf gdebi

# Install Hyper terminal
RUN wget -O hyper.deb https://releases.hyper.is/download/deb && \
    gdebi -n hyper.deb && \
    rm hyper.deb

# Install VSCode
RUN wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | apt-key add - && \
    apt-add-repository "deb https://packages.microsoft.com/repos/vscode stable main" && \
    apt update && \
    apt install -y code

# Install the most recent cmake
RUN apt install -y ca-certificates gnupg && \
    wget -q https://apt.kitware.com/keys/kitware-archive-latest.asc -O- | apt-key add - && \
    apt-add-repository "deb https://apt.kitware.com/ubuntu/ `lsb_release -cs` main" && \
    apt update && \
    apt install -y kitware-archive-keyring && \
    apt-key --keyring /etc/apt/trusted.gpg del C1F34CDD40CD72DA && \
    apt install -y cmake cmake-curses-gui

# Install graphics
RUN apt install -y xfce4 xfce4-goodies xserver-xorg-video-dummy xserver-xorg-legacy firefox
RUN sed -i 's/allowed_users=console/allowed_users=anybody/' /etc/X11/Xwrapper.config
COPY xorg.conf /etc/X11/xorg.conf

# We need the most recent x11vnc
RUN sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list && \
    apt update
RUN git clone https://github.com/LibVNC/x11vnc.git /opt/x11vnc && \
    cd /opt/x11vnc && \
    apt build-dep -y x11vnc && \
    autoreconf -fiv && \
    ./configure && \
    make && make install && \
    rm /opt/x11vnc -Rf

# Install Java
RUN apt install -y default-jdk

# Install Octave
RUN apt install -y octave epstool transfig

# Install markserv
RUN apt install -y nodejs npm
RUN npm install --global markserv

# Install jupyter
RUN apt install -y python3 python3-dev python3-pip python3-setuptools
RUN pip3 install ipython jupyter

# Install websockify
RUN git clone https://github.com/novnc/websockify.git /opt/websockify && \
    cd /opt/websockify && \
    python3 setup.py install

# Clone noVNC
RUN git clone https://github.com/novnc/noVNC.git /opt/novnc

# Install yarp dependencies
RUN echo "deb http://www.icub.org/ubuntu `lsb_release -cs` contrib/science" > /etc/apt/sources.list.d/icub.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 57A5ACB6110576A6
RUN apt update
RUN apt install -y icub-common

# Install Qt patch for Xfce
RUN apt install -y qml-module-qt-labs-folderlistmodel qml-module-qt-labs-settings

# Select branch + build type
ARG BRANCH=devel
ARG BUILD_TYPE=Release

# Build ycm
RUN git clone https://github.com/robotology/ycm.git
RUN cd ycm && mkdir build && cd build && \
    cmake .. \
    -DCMAKE_BUILD_TYPE=$BUILD_TYPE && \
    make install
RUN rm -Rf ycm

# Build robot-testing-framework
RUN git clone https://github.com/robotology/robot-testing-framework.git -b $BRANCH
RUN cd robot-testing-framework && mkdir build && cd build && \
    cmake .. \
    -DCMAKE_BUILD_TYPE=$BUILD_TYPE && \
    make install
RUN rm -Rf robot-testing-framework

# Build yarp
RUN git clone https://github.com/robotology/yarp.git
RUN cd yarp && mkdir build && cd build && \
    cmake .. \
    -DCMAKE_BUILD_TYPE=$BUILD_TYPE \
    -DYARP_COMPILE_libYARP_math=ON \
    -DYARP_COMPILE_CARRIER_PLUGINS=ON \
    -DYARP_COMPILE_DEVICE_PLUGINS=ON \
    -DYARP_COMPILE_GUIS=ON && \
    make install
RUN cp yarp/scripts/yarp_completion /etc/bash_completion.d/.
RUN rm -Rf yarp

# Build icub-main
RUN git clone https://github.com/robotology/icub-main.git -b $BRANCH
RUN cd icub-main && mkdir build && cd build && \
    cmake .. \ 
    -DCMAKE_BUILD_TYPE=$BUILD_TYPE \
    -DENABLE_icubmod_cartesiancontrollerserver=ON \
    -DENABLE_icubmod_cartesiancontrollerclient=ON \
    -DENABLE_icubmod_gazecontrollerclient=ON && \
    make install
RUN rm -Rf icub-main

# Build icub-contrib-common
RUN git clone https://github.com/robotology/icub-contrib-common.git
RUN cd icub-contrib-common && mkdir build && cd build && \
    cmake .. && \
    make install
RUN rm -Rf icub-contrib-common

ARG GITHUB_TOKEN

# Build audition-projects-helpers
RUN git config --global url."https://$GITHUB_TOKEN:@github.com/".insteadOf "https://github.com/"
RUN git clone https://github.com/dic-iit/audition-projects-helpers.git
RUN git config --global --remove-section url."https://$GITHUB_TOKEN:@github.com/"
RUN cd audition-projects-helpers && mkdir build && cd build && \
    cmake .. \
    -DCMAKE_BUILD_TYPE=$BUILD_TYPE && \
    make install
RUN rm -Rf audition-projects-helpers

# Set up .bashrc
RUN echo "PS1='\[\e]0;\u \w\a\]\[\033[01;32m\]\u\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \$ '" >> ~/.bashrc

# Set environmental variables
ENV DISPLAY=:1
ENV YARP_DATA_DIRS=/usr/local/share/yarp:/usr/local/share/iCub:/usr/local/share/ICUBcontrib
ENV LD_LIBRARY_PATH=/usr/local/lib:/usr/local/lib/yarp:/usr/local/lib/robottestingframework

# Set up Hyper launcher
COPY Hyper.desktop /root/Desktop/Hyper.desktop
RUN chmod +x /root/Desktop/Hyper.desktop

# Set up VSCode launcher
COPY ["Visual Studio Code.desktop", "/home/root/Desktop/Visual Studio Code.desktop"]
RUN chmod +x "/home/root/Desktop/Visual Studio Code.desktop"

# Manage markserv port
EXPOSE 8080

# Manage jupyter port
EXPOSE 8888

# Manage x11vnc port
EXPOSE 5901

# Manage noVNC port
EXPOSE 6080

# Manage yarp port
EXPOSE 10000/tcp 10000/udp

# Launch bash from /projects
WORKDIR /projects
CMD ["bash"]
