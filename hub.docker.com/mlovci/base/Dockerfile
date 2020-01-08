FROM ubuntu:16.04

MAINTAINER Michael Lovci <michaeltlovci@gmail.com>

RUN apt-get update && apt-get install -q -y wget libglib2.0-0 libsm6 libx11-dev libxrender1 libfontconfig1 libxext6 gcc ftp build-essential zlibc zlib1g zlib1g-dev openssl libssl-dev libmysqlclient-dev ghostscript zip emacs npm git curl libncurses5-dev default-jre default-jdk maven pandoc
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
