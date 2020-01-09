FROM alpine:latest

RUN apk add --no-cache ca-certificates curl
RUN mkdir /fivem
RUN curl https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/1809-99ec3f63d289f088f22872d0e54b64b1c2198aff/fx.tar.xz | tar xJ -C /fivem

WORKDIR /fivem

EXPOSE 30120/tcp 30120/udp

ENTRYPOINT ["sh", "/srv/run.sh"]
CMD ["+exec", "/srv/server.cfg"]