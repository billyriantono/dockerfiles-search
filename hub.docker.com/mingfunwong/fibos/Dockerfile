FROM ubuntu:16.04

RUN apt-get update -y \
  && apt-get install -y curl sudo openssl wget libusb-1.0-0 \
  && wget http://security.ubuntu.com/ubuntu/pool/main/i/icu/libicu55_55.1-7_amd64.deb \ 
  && dpkg -i libicu55_55.1-7_amd64.deb
