FROM ubuntu:16.04

# change apt-get sources to daumkakao server
ARG APTGET_SOURCE_KAKAO=1
RUN test "$APTGET_SOURCE_KAKAO" -eq 1 && \
    sed -i -e 's/archive.ubuntu.com/ftp.daumkakao.com/g' /etc/apt/sources.list && \
    sed -i -e 's/security.ubuntu.com/ftp.daumkakao.com/g' /etc/apt/sources.list && \
    sed -i -e 's/archive.canonical.com/ftp.daumkakao.com/g' /etc/apt/sources.list

# install minimal requirements
RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-utils && \
    apt-get install -y curl locales && \
    apt-get install -y build-essential

# set locale to UTF-8
RUN locale-gen "en_US.UTF-8"
RUN update-locale LANG=en_US.UTF-8
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en \
    LC_ALL=en_US.UTF-8
