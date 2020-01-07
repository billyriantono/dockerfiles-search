FROM ubuntu:bionic

ENV VERSION 6.1.5
ADD https://github.com/dbeaver/dbeaver/releases/download/${VERSION}/dbeaver-ce_${VERSION}_amd64.deb .

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
  apt-get install -y \
  openjdk-11-jre \
  libswt-gtk-4-jni \
  libswt-gtk-4-java \
  && \
  rm -rf /var/lib/apt/lists/* \
  && \
  dpkg -i dbeaver-ce_${VERSION}_amd64.deb

CMD dbeaver