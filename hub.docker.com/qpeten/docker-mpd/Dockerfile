FROM ubuntu:16.04
# Based on a Dockerfile from Scott Hansen
# https://github.com/firecat53/dockerfiles/blob/master/syncthing/Dockerfile

MAINTAINER Quentin Peten

ENV UID 1000
ENV GID 1000

RUN apt-get update -q && \
       apt-get install -qy mpd
RUN rm /etc/mpd.conf

RUN groupadd -g $GID mpd_user && \
       useradd --no-create-home -g mpd_user --uid $UID -G audio mpd_user

RUN mkdir -p /run/mpd/ && \
       chown mpd_user /run/mpd

USER mpd_user

CMD ["mpd", "--stdout", "--no-daemon", "/etc/mpd/mpd.conf"]
