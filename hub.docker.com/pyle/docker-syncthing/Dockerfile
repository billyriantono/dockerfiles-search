## Syncthing
## Author: Adam Pyle
## Project: Syncthing(https://github.com/syncthing/syncthing)

FROM alpine:3.4
MAINTAINER Adam Pyle <adam@pyle.xyz>
RUN apk add --update --no-cache openssl ca-certificates && update-ca-certificates
RUN wget http://github.com/syncthing/syncthing/releases/download/v0.14.14/syncthing-linux-amd64-v0.14.14.tar.gz -O /tmp/syncthing.tar.gz
RUN tar zxf /tmp/syncthing.tar.gz -C /tmp/ && rm -rf /tmp/syncthing.tar.gz && cp /tmp/syncthing*/syncthing /usr/local/bin/syncthing && rm -rf /tmp/syncthing*
VOLUME /root/.config/syncthing/
EXPOSE 8384
VOLUME /data
ENTRYPOINT ["/usr/local/bin/syncthing", "-gui-address=0.0.0.0:8384"]