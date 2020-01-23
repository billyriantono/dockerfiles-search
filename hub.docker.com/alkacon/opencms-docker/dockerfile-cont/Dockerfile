FROM ubuntu:16.04

MAINTAINER Alija Sabic <sabic.alija@gmail.com>

# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    mkdir -p /etc/sudoers.d && \	
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer


# Needed tools
RUN apt-get update && apt-get install -y \
    wget && \
    wget -qO - 'https://bintray.com/user/downloadSubjectPublicKey?username=openhab' | apt-key add - && \
    apt-get update && apt-get install -y \
    apt-transport-https && \
    echo 'deb https://dl.bintray.com/openhab/apt-repo2 stable main' | tee /etc/apt/sources.list.d/openhab2.list && \
    apt-get update && apt-get install -y \
    openhab2 openhab2-addons

# Install java
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java8-installer && \
    apt-get clean

# Expose openhab2 (default) port. Note: Apperantely not necessary.
# EXPOSE 8080

#USER developer
RUN alias ll='ls -la'
CMD ["/bin/bash"]
