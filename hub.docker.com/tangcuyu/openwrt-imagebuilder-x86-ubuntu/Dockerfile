FROM ubuntu:latest
LABEL maintainer="expo li<zzutcy@qq.com>"
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone
RUN cd /opt && apt-get update \
    && apt-get upgrade -y   
RUN apt-get install apt-utils \
    axel libncurses5-dev zlib1g-dev gawk \
    flex patch git-core g++ subversion xz-utils make unzip wget Python2.7 file -y \
    && apt-get clean
WORKDIR /opt/openwrt/
