FROM debian:jessie

RUN apt-get update && apt-get install -y gcc g++ build-essential devscripts cmake debhelper
RUN apt-get install -y dh-systemd dh-exec pkg-config libgles2-mesa-dev libasound2-dev libboost-all-dev
RUN apt-get install -y git