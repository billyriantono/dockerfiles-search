FROM jenkins:latest

USER root

RUN dpkg --add-architecture i386
RUN apt-get update && apt-get install -y build-essential gcc-multilib lib32stdc++6 lib32z1

USER jenkins