FROM golang:1.10
LABEL maintainer="Luka Hartwig <mail@lukahartwig.de>"

ENV DEP_VERSION 0.5.0

ADD https://github.com/golang/dep/releases/download/v${DEP_VERSION}/dep-linux-amd64 /usr/bin/dep
RUN chmod +x /usr/bin/dep

ENTRYPOINT [ "/usr/bin/dep" ]
