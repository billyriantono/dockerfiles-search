FROM ubuntu:18.04
RUN apt-get update \
  && apt-get install sudo curl vim libssl1.0.0 -y \
  && curl -s https://fibos.io/download/installer.sh | sh

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install vim net-tools lsof wget curl tmux traceroute
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install openssl ca-certificates && rm -rf /var/lib/apt/lists/*
