FROM cpswarm/stage-em-ex:latest

LABEL io.k8s.description="Stage Simulation Manager with Xfce desktop and headless VNC Environment" \
      io.k8s.display-name="cpswarm/stage-em-ex-vnc"

### Install some common tools for further installation, python-numpy is used for websockify/novnc
##  Install nss-wrapper to be able to execute image as non-root user
RUN apt-get update 

RUN apt-get install -y wget net-tools python-numpy libnss-wrapper gettext && apt-get clean -y

## Connection ports for controlling the UI:
# VNC port:5901
# noVNC webport, connect via http://IP:6901/?password=cpswarm
ENV HOME=/home \
	 DISPLAY=:1 \
    VNC_PORT=5901 \
    NO_VNC_PORT=6901
EXPOSE $VNC_PORT $NO_VNC_PORT

COPY . $HOME

### set up the option for vncserver, -SecurityTypes=None(default) for no authautication for vnc client connection, -SecurityTypes=VncAuth in contrast
ENV TERM=xterm \
    STARTUPDIR=$HOME/vncStartup \
    INST_SCRIPTS=$HOME/install \
    NO_VNC_HOME=$HOME/noVNC \
    DEBIAN_FRONTEND=noninteractive \
    VNC_COL_DEPTH=24 \
    VNC_RESOLUTION=1280x1024 \
    VNC_PW=cpswarm \
    SecurityTypes=None \
    VNC_VIEW_ONLY=false \
    RUNLEVEL=1

RUN $INST_SCRIPTS/set_user_permission.sh $STARTUPDIR $HOME $INST_SCRIPTS

RUN echo 'source $STARTUPDIR/generate_container_user' >> $HOME/.bashrc

WORKDIR $HOME

### Install xvnc-server & noVNC - HTML5 based VNC viewer
RUN $INST_SCRIPTS/tigervnc.sh
RUN $INST_SCRIPTS/no_vnc.sh

### Install xfce UI (windows manager)
RUN $INST_SCRIPTS/xfce_ui.sh && apt-get -y autoremove

USER 1000

ENTRYPOINT ["/home/vncStartup/vnc_startup.sh"]
CMD ["--wait"]




