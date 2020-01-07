FROM node
MAINTAINER ngiy

RUN apt update
RUN apt install -y python-dev python-pip jq curl zip rsync
RUN pip install awscli

ENV VER="18.09.2"

RUN set -x
RUN curl -L -o /tmp/docker-$VER.tgz https://download.docker.com/linux/static/stable/x86_64/docker-$VER.tgz
RUN tar -xz -C /tmp -f /tmp/docker-$VER.tgz
RUN mv /tmp/docker/* /usr/bin

RUN curl https://raw.githubusercontent.com/silinternational/ecs-deploy/master/ecs-deploy | tee /usr/local/bin/ecs-deploy
RUN chmod +x /usr/local/bin/ecs-deploy

RUN curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb"
RUN dpkg -i session-manager-plugin.deb

COPY config /root/.ssh/config
