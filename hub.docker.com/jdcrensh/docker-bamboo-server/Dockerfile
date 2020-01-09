FROM alpine

ENV BAMBOO_VERSION 5.14.1
ENV BAMBOO_HOME /var/bamboo
ENV BAMBOO_INSTALL_DIR /opt/bamboo
ENV DOWNLOAD_URL https://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-${BAMBOO_VERSION}.tar.gz

RUN apk update && apk upgrade
RUN apk add bash curl tar git nodejs openssh openjdk8

RUN mkdir -p $BAMBOO_INSTALL_DIR
RUN curl -L --silent ${DOWNLOAD_URL} | tar -xz --strip=1 -C "$BAMBOO_INSTALL_DIR"

EXPOSE 8085
EXPOSE 54663

VOLUME ["$BAMBOO_HOME"]

WORKDIR $BAMBOO_INSTALL_DIR
CMD ./bin/start-bamboo.sh -fg

