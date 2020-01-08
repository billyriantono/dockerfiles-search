FROM ubuntu:16.04
MAINTAINER David Bautista <dbautistav@gmail.com>

RUN apt-get update
RUN apt-get dist-upgrade -y
RUN apt-get install -y build-essential libssl-dev
RUN apt-get install -y git-core git
RUN apt-get install -y curl nano vim wget
RUN apt-get install -y fontconfig htop tmux zsh
RUN apt-get autoremove -y

CMD ["/bin/bash", "-c"]
