FROM lsiobase/alpine:3.10

LABEL maintainer="aptalca"

RUN \
 echo "**** install runtime packages ****" && \
 apk add --no-cache --upgrade \
        openssh-server && \
 echo "**** setup openssh environment ****" && \
 sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config && \
 ssh-keygen -A && \
 rm -rf \
        /tmp/*

# add local files
COPY /root /