FROM alpine:3.4

ENV GOPATH /go
ENV PATH $PATH:/go/bin

RUN echo "@community http://nl.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN apk update && \
    apk -v --virtual build-deps add git make go@community musl-dev && \
    apk -v add bash go@community && \
    go version

COPY ./build.sh /bin/build.sh

ENTRYPOINT ["/bin/build.sh"]
CMD [""]




