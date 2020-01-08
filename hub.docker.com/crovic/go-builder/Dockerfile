FROM golang:1.9

VOLUME /src
WORKDIR /src

COPY build_env.sh /
COPY build.sh /

ENTRYPOINT ["/build.sh"]
