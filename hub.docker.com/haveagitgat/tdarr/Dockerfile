FROM ubuntu:18.04

# Replace 1000 with your user / group id

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y git-core subversion build-essential gcc-multilib sudo

RUN export uid=1000 gid=1000 && \
    mkdir -p /home/Tdarr && \
    mkdir -p /home/Tdarr/media && \
    mkdir -p /home/Source && \	
    echo "Tdarr:x:${uid}:${gid}:Tdarr,,,:/home/Tdarr:/bin/bash" >> /etc/passwd && \
    echo "Tdarr:x:${uid}:" >> /etc/group && \
    echo "Tdarr ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/Tdarr && \
    chmod 0440 /etc/sudoers.d/Tdarr && \
    chown ${uid}:${gid} -R /home/Tdarr


RUN apt-get install dbus-x11 packagekit-gtk3-module libcanberra-gtk-module -y
RUN apt-get install dbus libnotify4 libnss3 libxss1 xdg-utils trash-cli  trash-cli libglib2.0-bin gvfs-bin -y

RUN apt install curl
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
RUN apt install nodejs




RUN apt-get install -y software-properties-common && apt-get update
RUN add-apt-repository ppa:jonathonf/ffmpeg-4 && apt-get update && apt-get -y install ubuntu-restricted-extras
RUN apt-get -y install handbrake-cli ffmpeg libavcodec-extra libdvdnav4 libdvdread4 libavcodec-extra57 gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly ubuntu-restricted-extras

RUN sudo mkdir -p /data/db
RUN sudo apt install -y mongodb-server  


USER Tdarr
ENV HOME /home/Tdarr

RUN chown ${uid}:${gid} -R /home/Source
WORKDIR /home/Source
RUN sudo mkdir -p /home/Source/Tdarr
RUN sudo git clone https://github.com/HaveAGitGat/Tdarr
WORKDIR /home/Source/Tdarr

RUN curl https://install.meteor.com/ | sh

RUN sudo npm install --production
RUN sudo meteor build --server localhost:8265 --directory /home/Source/Build/Tdarr --architecture os.linux.x86_64 --allow-superuser
WORKDIR /home/Source/Build/Tdarr/bundle/programs/server
RUN sudo npm install



CMD sudo service mongodb start && \
 echo "Mongo started, waiting 10 seconds" && \
 sleep 10 && \
 echo "Tdarr started" && \
 sudo MONGO_URL=mongodb://localhost:27017/Tdarr PORT=8265 ROOT_URL=http://localhost/ node /home/Source/Build/Tdarr/bundle/main.js







