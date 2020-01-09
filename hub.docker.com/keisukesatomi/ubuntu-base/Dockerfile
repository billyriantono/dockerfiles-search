FROM ubuntu:18.04 

MAINTAINER Keisuke Satomi <satomi@fignny.co.jp>

WORKDIR /root

ENV DEBIAN_FRONTEND=noninteractive
# timezone
ENV TZ=Asia/Tokyo

RUN apt update \
&& apt upgrade -y \
&& apt install -y git vim curl locales zip unzip\
&& locale-gen en_US.UTF-8 \
&& echo "export LANG=en_US.UTF-8" >> ~/.bashrc

# Don't merge to upper code. Install of tzdata needs to be isolated.
RUN apt install -y tzdata

