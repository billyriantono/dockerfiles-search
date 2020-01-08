# To Run:
# OSX:  (using Xquartz)
# DISPLAY=`hostname`:0
#xhost +
#docker run --rm --net=host -e DISPLAY=$DISPLAY -v $HOME/temp/firefox:/config:rw -v /tmp/.X11-unix:/tmp/.X11-unix --volume="$HOME/.Xauthority:/root/.Xauthority:rw" -v /Users/dtranquada/.xiphos:/root/.xiphos -v /Users/dtranquada/.sword:/root/.sword xiphos

FROM ubuntu:18.04
MAINTAINER Admatic Engineering Team@ADMATIC.IN

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y install locales
RUN locale-gen en_US.UTF-8
RUN locale-gen 
RUN  LC_ALL="en_US.UTF-8" LANG="en_US.UTF-8" dpkg-reconfigure locales
RUN export LC_ALL="en_US.UTF-8"
RUN export LANG="en_US.UTF-8"
RUN apt-get install -y xiphos

ENTRYPOINT ["/usr/bin/xiphos"]
