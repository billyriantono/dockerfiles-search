FROM ros:kinetic-robot-xenial

# Setup the vncserver from consol
## Connection ports for controlling the UI:
# VNC port:5901
# noVNC webport, connect via http://IP:6901/?password=vncpassword
ENV DISPLAY=:1 \
    VNC_PORT=5901 \
    NO_VNC_PORT=6901
EXPOSE $VNC_PORT $NO_VNC_PORT

### Envrionment config
ENV USER=ros_user 
ENV	HOME=/home/$USER \
    TERM=xterm \
    STARTUPDIR=/dockerstartup \
    INST_SCRIPTS=$HOME/install \
    NO_VNC_HOME=$HOME/noVNC \
    DEBIAN_FRONTEND=noninteractive \
    VNC_COL_DEPTH=24 \
    VNC_RESOLUTION=1280x768 \
    VNC_PW=vncpassword \
    VNC_VIEW_ONLY=false

RUN useradd -ms /bin/bash -g sudo $USER

### Add all install scripts for further steps
ADD ./install/common/install/ $INST_SCRIPTS/
ADD ./install/ubuntu/install/ $INST_SCRIPTS/
RUN find $INST_SCRIPTS -name '*.sh' -exec chmod a+x {} +

### Install some common tools
RUN $INST_SCRIPTS/tools.sh
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

### Install xvnc-server & noVNC - HTML5 based VNC viewer
RUN $INST_SCRIPTS/tigervnc.sh
RUN $INST_SCRIPTS/no_vnc.sh

### Install chrome
RUN $INST_SCRIPTS/chrome.sh

### Install xfce UI
RUN $INST_SCRIPTS/xfce_ui.sh
ADD ./install/common/xfce/ $HOME/

RUN $INST_SCRIPTS/libnss_wrapper.sh
ADD ./install/common/scripts $STARTUPDIR
RUN $INST_SCRIPTS/set_user_permission.sh $STARTUPDIR $HOME

## Install Visual studio code
RUN $INST_SCRIPTS/install_vscode.sh

# Change password
RUN echo "$USER:$USER" | chpasswd

# Go into user
USER $USER
WORKDIR /home/$USER

# Source ros 
RUN echo "source /opt/ros/kinetic/setup.bash" >> $HOME/.bashrc

# Add the repos needed
# RUN $INST_SCRIPTS/comp0037_repos.sh

ENTRYPOINT ["/dockerstartup/vnc_startup.sh"]
CMD ["bash"]
