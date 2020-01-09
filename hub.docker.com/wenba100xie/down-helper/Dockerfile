FROM alpine:latest
#RUN sed -i "s@http://dl-cdn.alpinelinux.org/@https://mirrors.huaweicloud.com/@g" /etc/apk/repositories
#RUN apk update
RUN apk add wget vim git curl

RUN mkdir /down

WORKDIR /down


RUN git clone "https://gerrit.asterisk.org/asterisk"
RUN git clone git://git.asterisk.org/dahdi/linux
RUN git clone git://git.asterisk.org/dahdi/tools
RUN git clone "https://gerrit.asterisk.org/libpri"
RUN git clone "https://gerrit.asterisk.org/libss7"
RUN git clone https://stash.freeswitch.org/scm/fs/freeswitch.git

