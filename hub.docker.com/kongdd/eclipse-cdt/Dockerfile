FROM ubuntu:16.04
MAINTAINER Dongdong Kong "kongdd.sysu@gmail.com"

RUN apt-get update && apt-get install -y \
    software-properties-common \
    default-jre libxext-dev libxrender-dev libxtst-dev \
    wget \
    libgtk2.0-0 libcanberra-gtk-module \
    g++ libboost-all-dev build-essential gdb && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

RUN wget http://archive.eclipse.org/technology/epp/downloads/release/helios/SR2/eclipse-cpp-helios-SR2-linux-gtk-x86_64.tar.gz \
    -O /tmp/eclipse.tar.gz -q && \
    tar -xf /tmp/eclipse.tar.gz -C /opt && \
    rm /tmp/eclipse.tar.gz

ADD run /usr/local/bin/eclipse

RUN chmod +x /usr/local/bin/eclipse && \
    useradd -ms /bin/bash developer

# RUN mkdir -p /home/developer && \
#     chown developer:developer -R /home/developer && \
#     chown root:root /usr/bin/sudo && chmod 4755 /usr/bin/sudo

USER developer
ENV HOME /home/developer
WORKDIR /home/developer
CMD /usr/local/bin/eclipse
