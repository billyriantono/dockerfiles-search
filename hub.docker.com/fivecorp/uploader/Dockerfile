FROM golang:1.13

ADD   . /opt/src
WORKDIR /opt/src

RUN go get -t ./...
RUN cd /opt/src/cmd/bootstrap && go build
RUN cd /opt/src/cmd/update    && go build
RUN cd /opt/src/cmd/uploader  && go build

FROM azul/zulu-openjdk:8

# Add wget and unzip to help install dependencies
RUN DEBIAN_FRONTEND=NONINTERACTIVE apt-get update -q && \
    apt-get install -y wget unzip

COPY --from=0 /opt/src/cmd/bootstrap/bootstrap /usr/bin/bootstrap
COPY --from=0 /opt/src/cmd/update/update       /usr/bin/update
COPY --from=0 /opt/src/cmd/uploader/uploader   /usr/bin/uploader
COPY templates/ /opt/templates

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

VOLUME /opt/uploader
CMD ["/usr/bin/uploader", "-config", "/opt/uploader/config"]
