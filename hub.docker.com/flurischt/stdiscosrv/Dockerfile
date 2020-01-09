FROM ubuntu:xenial

USER root

RUN useradd -d "/home/stdiscosrv" -u 1001 -m -s /bin/bash stdiscosrv
WORKDIR /home/stdiscosrv

# need apt-transport to use syncthing repository
RUN apt-get update && apt-get install -y apt-transport-https ca-certificates curl

# Install syncthing from repository
RUN curl -s https://syncthing.net/release-key.txt | apt-key add -
RUN echo "deb https://apt.syncthing.net/ syncthing stable" | tee /etc/apt/sources.list.d/syncthing.list

RUN apt-get update && apt-get install -y syncthing-discosrv

USER stdiscosrv

EXPOSE 8443

CMD ["/usr/bin/stdiscosrv", "-http"]
