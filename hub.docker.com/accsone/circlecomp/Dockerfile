# circlcomp
#
# VERSION               1.0.0

FROM      kurento/kurento-media-server:6.2.1
MAINTAINER accSone <email@accsone.com>

#update libnice
RUN apt-get -y update 
RUN apt-get -y upgrade
RUN apt-get -y dist-upgrade

COPY ./deb/circlecomp_0.0.1~rc1_amd64.deb /circlecomp_0.0.1~rc1_amd64.deb
RUN dpkg -i /circlecomp_0.0.1~rc1_amd64.deb

#EXPOSE 8888 49152-65535/udp 3478/udp 3478 19302/udp 19302
EXPOSE 8888 49152-50000/udp 3478/udp 3478 19302/udp 19302

