
FROM buildpack-deps:bionic
MAINTAINER Christian Geymonat chris.geymo@gmail.com

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y sudo zip unzip python-dev && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
 
RUN adduser --disabled-password --gecos '' developer
RUN adduser developer sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER developer
WORKDIR /home/developer
ADD ./init.sh init.sh
RUN /bin/bash init.sh
#RUN source "$HOME/.sdkman/bin/sdkman-init.sh"