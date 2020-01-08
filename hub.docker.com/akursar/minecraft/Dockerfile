FROM phusion/baseimage:0.9.15

ENV HOME /root

RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

CMD ["/sbin/my_init"]

ENV    DEBIAN_FRONTEND noninteractive

RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/cache/oracle-jdk8-installer

RUN mkdir /var/lib/minecraft
RUN curl -s "https://s3.amazonaws.com/Minecraft.Download/versions/1.8.1/minecraft_server.1.8.1.jar" -o /var/lib/minecraft/minecraft_server.jar
RUN echo "eula=true" > /var/lib/minecraft/eula.txt

RUN mkdir /etc/service/minecraft
ADD minecraft.sh /etc/service/minecraft/run

EXPOSE 25565

VOLUME ["/minecraft"]

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
