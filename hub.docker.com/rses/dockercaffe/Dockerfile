FROM bvlc/caffe:gpu

MAINTAINER Twin Karmakharm <t.karmakharm@sheffield.ac.uk>


RUN apt-get update && apt-get install -y bsdmainutils imagemagick vim nano

# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/ubuntu && \
    mkdir -p /etc/sudoers.d && \
    echo "ubuntu:x:${uid}:${gid}:Ubuntu,,,:/home/ubuntu:/bin/bash" >> /etc/passwd && \
    echo "ubuntu:x:${uid}:" >> /etc/group && \
    echo "ubuntu ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/ubuntu && \
    chmod 0440 /etc/sudoers.d/ubuntu && \
    chown ${uid}:${gid} -R /home/ubuntu

USER ubuntu
ENV HOME /home/ubuntu
WORKDIR /home/ubuntu
