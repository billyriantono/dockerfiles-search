
FROM ysaotome/ubuntu

MAINTAINER Yuichi Saotome <y@sotm.jp>

# Install Middleware
ENV DEBIAN_FRONTEND noninteractive
## Add node Repo
RUN wget -qO- https://deb.nodesource.com/setup | bash -
RUN apt-get update
RUN apt-get install -y supervisor redis-server openssh-server nodejs
RUN apt-get clean

# Install Hubot
RUN npm install -g hubot@2.6.0 coffee-script
WORKDIR /
RUN hubot --create Hubot-DevHub
WORKDIR /Hubot-DevHub
RUN npm install hubot-devhub --save
RUN npm install .

# Set sshd
## Add hubot user
RUN useradd -m -d /Hubot-DevHub -s /bin/bash hubot
RUN echo 'hubot:hubot' | chpasswd
RUN echo 'hubot ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/hubot
RUN mkdir /var/run/sshd

ENV HUBOT_DEVHUB_NAME hubot
ENV HUBOT_DEVHUB_URL http://localhost:3000/

ADD supervisord.conf /etc/supervisor/conf.d/hubot-devhub.conf

EXPOSE 22 
VOLUME ["/Hubot-DevHub", "/var/lib/redis"]

ENTRYPOINT ["/usr/bin/supervisord", "-n"]

