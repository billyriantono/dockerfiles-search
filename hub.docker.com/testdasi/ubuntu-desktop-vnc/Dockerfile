# This Dockerfile is used to build an headles vnc image based on Ubuntu

FROM ubuntu:latest
MAINTAINER testdasi
# ENV REFRESHED_AT 2019-06-01

LABEL io.k8s.description="Headless VNC Container with Xfce window manager, firefox and chromium" \
      io.k8s.display-name="Headless VNC Container based on Ubuntu" \
      io.openshift.expose-services="6901:http,5901:xvnc" \
      io.openshift.tags="vnc, ubuntu, xfce" \
      io.openshift.non-scalable=true

## Connection ports for controlling the UI:
# VNC port:5901
# noVNC webport, connect via http://IP:6901/?password=vncpassword
ENV DISPLAY=:1 \
    VNC_PORT=5901 \
    NO_VNC_PORT=6901
EXPOSE $VNC_PORT $NO_VNC_PORT

### Envrionment config
ENV HOME=/headless \
    TERM=xterm \
    STARTUPDIR=/dockerstartup \
    INST_SCRIPTS=/headless/install \
    NO_VNC_HOME=/headless/noVNC \
    DEBIAN_FRONTEND=noninteractive \
    VNC_COL_DEPTH=24 \
    VNC_RESOLUTION=1280x1024 \
    VNC_PW=vncpassword \
    VNC_VIEW_ONLY=false
WORKDIR $HOME

### Add all install scripts for further steps
ADD ./install/ $INST_SCRIPTS/
RUN find $INST_SCRIPTS -name '*.sh' -exec chmod a+x {} +

### Install prerequisites and set language to UK because I'm posh like that
RUN $INST_SCRIPTS/prerequisite.sh
ENV LANG='en_GB.UTF-8' LANGUAGE='en_GB:en' LC_ALL='en_GB.UTF-8'

### Install desktop GUI
RUN $INST_SCRIPTS/desktopgui.sh

### Install apps
RUN $INST_SCRIPTS/apps.sh

### configure startup
RUN $INST_SCRIPTS/postsscript.sh
ADD ./startup/ $STARTUPDIR
RUN $INST_SCRIPTS/set_user_permission.sh $STARTUPDIR $HOME

USER 1000

ENTRYPOINT ["/dockerstartup/vnc_startup.sh"]
CMD ["--wait"]
