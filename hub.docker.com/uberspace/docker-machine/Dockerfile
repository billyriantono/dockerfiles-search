FROM golang as go
ENV CGO_ENABLED=0
RUN go get github.com/docker/machine/cmd/docker-machine

FROM scratch
COPY --from=go /go/bin/docker-machine /go/bin/
CMD ["/go/bin/docker-machine"]
