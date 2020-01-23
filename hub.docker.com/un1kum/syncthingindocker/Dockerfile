FROM ubuntu:14.04
MAINTAINER Vitalii Golovanev <v.golovanev@gmail.com>
ADD https://syncthing.net/release-key.txt /root/key
RUN sudo apt-key add /root/key
RUN echo "deb http://apt.syncthing.net/ syncthing release" | sudo tee /etc/apt/sources.list.d/syncthing.list
RUN sudo apt-get update
RUN sudo apt-get install syncthing
ENTRYPOINT syncthing
EXPOSE 8384 22000 21015/udp 21027/udp