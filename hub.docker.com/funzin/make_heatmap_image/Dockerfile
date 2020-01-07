FROM ubuntu:18.04
MAINTAINER funzin<nakazawa.fumito@gmail.com>

# Copy local MakeHeatMapImage
ARG dir="/experiment/MakeHeatMapImage/"
RUN mkdir -p $dir
COPY ./ $dir
WORKDIR $dir
RUN rm -rf output/ tmp/

# node, npm, imagemagick
RUN apt-get update
RUN apt-get install -y sudo
RUN sudo apt-get install -y nodejs npm wget curl imagemagick
RUN sudo npm cache clean
RUN sudo npm install n -g
RUN sudo n 10.11.0
RUN sudo ln -sf /usr/local/bin/node /usr/bin/node
RUN sudo apt-get purge -y nodejs npm
RUN sudo npm update -g npm

# install package.json
RUN npm install
