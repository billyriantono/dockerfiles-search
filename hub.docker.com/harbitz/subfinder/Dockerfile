FROM golang:1.13.4-alpine3.10 AS build
RUN apk --no-cache add git openssh-client ca-certificates
RUN go get github.com/subfinder/subfinder; exit 0
WORKDIR /go/src/github.com/subfinder/subfinder
RUN go install ./...

FROM alpine:latest
COPY run.sh .
RUN mkdir /output
RUN apk --no-cache add ca-certificates
COPY --from=build /go/bin/subfinder /bin/subfinder
ENV HOME /
ENTRYPOINT ["/run.sh"]