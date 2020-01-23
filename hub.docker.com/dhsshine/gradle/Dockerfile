FROM gradle:5.2.0-jdk8

USER root
RUN apt update && apt install sudo -y
RUN adduser gradle sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER gradle
