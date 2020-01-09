FROM alpine:3.5
MAINTAINER billypon

RUN apk add --no-cache syncthing && \
    mkdir -p ~/.config && \
    ln -s /home/syncthing/.config ~/.config/syncthing

WORKDIR /home/syncthing
EXPOSE 8384 22000 21027/udp
VOLUME ["/home/syncthing"]
CMD ["syncthing", "-logflags=3"]
