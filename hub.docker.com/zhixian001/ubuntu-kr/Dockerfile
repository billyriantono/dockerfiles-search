# Author: JHYeom
# Pull base image.
FROM ubuntu:20.04
LABEL maintainer="zhixian001"\
      version="1.0"

ENV TZ=Asia/Seoul

# Install locale.(with daumkakao repository)
RUN \
  sed -i 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list && \
  ln -sf "/usr/share/zoneinfo/${TZ}" /etc/localtime && \
  echo "${TZ}" > /etc/timezone && \
  apt-get update && \
  apt-get install -y locales tzdata && \
  rm -rf /var/lib/apt/lists/* && \
  locale-gen ko_KR.UTF-8
# set locale
ENV LC_ALL=ko_KR.UTF-8
ENTRYPOINT [ "/bin/bash" ]
