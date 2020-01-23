FROM alpine
LABEL maintainer="Bartosz Gadzala <bartosz.gadzala@gmail.com>"

ENV URL "https://downloads.sourceforge.net/project/freemind/freemind/1.0.1/freemind-bin-max-1.0.1.zip"

WORKDIR /home/freemind
RUN apk update && apk upgrade && apk add \
     openjdk8-jre \
     ttf-dejavu \
     fontconfig \
     wget && \
     wget --quiet $URL -O fm.zip && \
     unzip fm.zip && rm fm.zip && \
     chmod +x freemind.sh

ADD fmexport.sh /usr/bin/fmexport
RUN chmod +x /usr/bin/fmexport