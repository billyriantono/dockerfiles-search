FROM golang:latest

RUN apt-get update \
&& apt-get install -y \
  qemu-user \
  qemu-user-static \
  build-essential \
  crossbuild-essential-arm64 \
  crossbuild-essential-armel \
  crossbuild-essential-armhf \
&& apt-get clean --yes
