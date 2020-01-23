# Migration to Bitbucket
FROM alpine:latest

MAINTAINER Nicolas Zagulajew (freeeflyer) <docker.com@xoop.org>

ENV RS_HOME=/var/rs
ENV RS_VERSION=3.5.4

RUN echo "Installing dependencies.." 
RUN apk update && apk add bash 
RUN echo "Downloading RadicalSpam.."
# http://www.radical-spam.org/download/radicalspam_v3.5.4/radicalspam-server-3.5.4.tar.gz
ADD http://www.radical-spam.org/download/radicalspam_v$RS_VERSION/radicalspam-server-$RS_VERSION.tar.gz /tmp/radicalspam-server-stable.tar.gz

#RUN echo "Checking md5" && \
#  cd /tmp && \
#  md5sum -c radicalspam-server-stable.tar.gz.md5 

RUN echo "Installing RadicalSpam " && \
  cd /usr/share && \
  tar --numeric-owner -xzf /tmp/radicalspam-server-stable.tar.gz && \
  rm /tmp/radicalspam-server-stable.tar.gz && \
  ln -sf /usr/share/rs /var/rs


ENV PATH=/var/rs/etc/scripts:$PATH 
    

VOLUME ["/data" ]

WORKDIR $RS_HOME

CMD ["sh", "-c", "while /bin/true; do sleep 60; done"]

EXPOSE 25




