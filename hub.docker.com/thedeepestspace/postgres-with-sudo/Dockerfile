FROM postgres:latest

USER root
RUN apt-get update && apt-get -y install sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN service sudo restart
RUN adduser postgres sudo
