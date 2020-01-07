FROM ubuntu:18.04

# Set host time zone 
ENV TZ=Asia/Bangkok
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install package 
RUN apt-get update -y \
    && apt-get install -y ca-certificates \
    gnupg2 \
    wget \
    openssh-server \
    jq \
    zip