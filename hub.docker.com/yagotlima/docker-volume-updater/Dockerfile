FROM busybox:1.29
LABEL maintainer="Yago Toledo Lima <yagotoledolima@gmail.com>"

VOLUME /destination-volume

COPY data /data
COPY entrypoint.sh /usr/local/bin/

ENTRYPOINT [ "sh", "-c", "entrypoint.sh" ]
