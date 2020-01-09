# Set base
FROM gcc

# Dockerfile author
MAINTAINER Stdgregwar <gregoirehirt@gmail.com>

# Update & install env
RUN echo "deb http://ftp.fr.debian.org/debian testing main" >> /etc/apt/sources.list
RUN apt-get update --yes
RUN apt-get install --yes cmake xvfb libluajit-5.1-dev libphysfs-dev libopenal-dev libmodplug-dev libvorbis-dev qtbase5-dev qttools5-dev qttools5-dev-tools libsdl2-dev libsdl2-ttf-dev libsdl2-image-dev libglm-dev

