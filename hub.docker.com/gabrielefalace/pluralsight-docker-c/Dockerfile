FROM alpine:edge

MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="The NEM Infrastructure Server (NIS) Docker image based on Alpine linux"

WORKDIR /tmp

# packages
RUN apk add --update --no-cache \
  "openjdk8-jre" \
  "bash"

# build deps
RUN apk --no-cache --virtual .build-deps add \
  "wget" \
  "unzip"

# nis-ncc install
RUN wget http://bob.nem.ninja/last-ncc/nis-ncc-0.6.91.tgz && \
  tar xvzf nis-ncc-0.6.91.tgz && \
  rm -v nis-ncc-0.6.91.tgz

RUN mv -v package/* /tmp && \
  rmdir -v package

# cleanup
RUN apk del --purge .build-deps

EXPOSE 7890
EXPOSE 8989

CMD ["./nix.runNis.sh"]
