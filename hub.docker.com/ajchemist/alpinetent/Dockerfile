FROM ubuntu:bionic
MAINTAINER Noctis <urakiny@gmail.com>
RUN apt update && apt install -y python python-dev python-pip && apt clean && apt autoclean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir -p /app
WORKDIR /app
EXPOSE 80
CMD ["bash"]