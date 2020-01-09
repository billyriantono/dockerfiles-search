FROM debian:jessie
MAINTAINER JeffreyH89 <mail@mail.com>

RUN apt-get update && apt-get install -y wget libfontconfig1 libfreetype6 liblzo2-2 libpng12-0 libsdl1.2debian unzip
WORKDIR /opt
RUN wget https://binaries.openttd.org/releases/1.6.1/openttd-1.6.1-linux-generic-amd64.tar.gz
RUN tar xvf openttd-1.6.1-linux-generic-amd64.tar.gz
WORKDIR /opt/openttd-1.6.1-linux-generic-amd64/baseset
RUN wget http://bundles.openttdcoop.org/opengfx/releases/LATEST/opengfx-0.5.4.zip
RUN unzip opengfx-0.5.4.zip
WORKDIR /opt/openttd-1.6.1-linux-generic-amd64

EXPOSE 3979/tcp
EXPOSE 3979/udp

ENTRYPOINT ["./openttd"]
CMD ["-D"]
