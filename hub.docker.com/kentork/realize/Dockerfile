FROM golang:1.11-alpine
RUN apk add --no-cache git \
    && go get -u github.com/tockins/realize \
    && apk del --purge git

ENTRYPOINT ["realize"]
CMD ["-v"]
