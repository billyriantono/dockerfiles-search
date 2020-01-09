# Docker-tftpd
FROM ubuntu:18.04

MAINTAINER Shawn Groberg

# Build container
#   docker build -t sgroberg/tftpd 

# Start the container with the follonwing command:
#   docker service create  --name tftpd  -v $(pwd):/var/lib/tftpboot  sgroberg/tftpd

# Install tftpd-hpa deamon -*1
RUN apt-get update
RUN apt-get install -y tftpd-hpa
VOLUME /var/lib/tftpboot

CMD systemctl enable tftpd-hpa
CMD systemctl restart tftpd-hpa 

EXPOSE 69/udp

ENTRYPOINT /etc/init.d/tftpd-hpa start && bash
