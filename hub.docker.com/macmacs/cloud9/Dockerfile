# Cloud9 server
# A lot inspired by https://hub.docker.com/r/gai00/cloud9/~/dockerfile/
#                   https://hub.docker.com/r/kdelfour/cloud9-docker/~/dockerfile/

FROM node:6-slim
MAINTAINER Antoine GIRARD <antoine.girard@sapk.fr>

RUN \
  buildDeps='make build-essential g++ gcc python2.7' && softDeps="git util-linux bash" \
  && apt-get update && apt-get upgrade -y \
  && apt-get install -y sudo tmux graphicsmagick libmagickwand-dev nano htop vnstat imagemagick ssh locales $buildDeps $softDeps --no-install-recommends

RUN \
 apt-get autoremove -y && apt-get autoclean -y && apt-get clean -y \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && npm install -g forever && npm cache clean
 
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

RUN \
 curl -sSL https://get.rvm.io | bash -s stable --ruby --gems=jekyll,bundler,rmagick,exifr\
 && git clone https://github.com/c9/core.git /cloud9 && cd /cloud9 \
 && scripts/install-sdk.sh \

RUN npm cache clean

RUN useradd -m docker -s /bin/bash && echo "docker:docker" | chpasswd \
	&& adduser docker sudo \
	&& echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers \
	&& mkdir /home/docker/ -p -v \
	&& chown docker:docker /home/docker/ -R \
	&& chown docker:docker /usr/local/rvm/ -R \
	&& locale-gen en_US.UTF-8 \
    && localedef -i en_GB -f UTF-8 en_US.UTF-8
	
# Install c9 dependencies
RUN curl -L https://raw.githubusercontent.com/c9/install/master/install.sh | bash

VOLUME /workspace
EXPOSE 8181 
ENTRYPOINT ["forever", "/cloud9/server.js", "-w", "/workspace", "-l", "0.0.0.0"]