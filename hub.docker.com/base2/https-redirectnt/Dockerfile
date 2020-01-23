FROM kalilinux/kali-linux-docker:latest

MAINTAINER Xavi Torelló <info@xaviertorello.cat>

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm-256color

RUN rm -fR /var/lib/apt/
RUN apt-get clean
RUN apt-get update -y
RUN apt-get upgrade -y

CMD ["/bin/bash"]
