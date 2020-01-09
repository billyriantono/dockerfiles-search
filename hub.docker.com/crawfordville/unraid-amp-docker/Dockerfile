FROM ubuntu:16.04

## install dependencies
RUN mkdir -p /usr/share/man/man1 \
&& apt-get update && apt-get -y install \
tzdata \
screen \
socat \
tmux \
libsqlite3-dev \
lib32stdc++6 \
lib32gcc1 \
git \
wget \
coreutils \
unzip \
iputils-ping \
netcat \
openjdk-8-jre-headless

## make the amp user
RUN useradd -d /home/amp -s /bin/bash -m amp
WORKDIR /home/amp

## expose required ports
EXPOSE 25565 8080

RUN wget https://cubecoders.com/Downloads/ampinstmgr.zip \
&& unzip ampinstmgr.zip \
&& rm ampinstmgr.zip

COPY start.sh .
RUN chmod +x start.sh


## create required volumes
RUN mkdir /home/amp/server_data \
&& ln -vs /home/amp/.ampdata/instances/${MODULE} /home/amp/server_data
VOLUME ["/home/amp/server_data"]


USER amp

## configure the container process
CMD ["/bin/bash", "/home/amp/start.sh"]
