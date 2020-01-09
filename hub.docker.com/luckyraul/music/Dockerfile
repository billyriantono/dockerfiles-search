FROM node:12-buster-slim

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -qqy update && apt-get -qy install davfs2 gettext-base
RUN npm install -g mstream

RUN mkdir -p /music/disk && \
    touch /etc/davfs2/secrets && \
    echo '/music/disk $DISKUSER $DISKPWD' >> /etc/davfs2/secrets && \
    chmod 400 /etc/davfs2/secrets && \
    echo 'https://webdav.yandex.ru  /music/disk davfs noauto,user 0 0' >> /etc/fstab

EXPOSE 3000

ADD entrypoint.sh .
RUN chmod +x /entrypoint.sh

WORKDIR /music
CMD mstream

ENTRYPOINT ["/entrypoint.sh"]
