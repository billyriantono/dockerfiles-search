FROM golang:1.10 as builder
RUN apt-get update -y && apt-get install -yqq libtool
WORKDIR /go/src/app
COPY . .
RUN go get -d -v ./...
RUN go build main.go

ADD https://download.docker.com/linux/static/stable/x86_64/docker-18.03.1-ce.tgz /docker.tgz
RUN tar xzf /docker.tgz
RUN cp docker/docker /usr/bin

# Run with docker run -v /var/run/docker.sock:/var/run/docker.sock fwilhe/golang-experiments
FROM gcr.io/distroless/base
COPY --from=builder /usr/lib/x86_64-linux-gnu/libltdl.so.7 /usr/lib/x86_64-linux-gnu/
COPY --from=builder /go/src/app/main /
COPY --from=builder /usr/bin/docker /usr/bin/
ENTRYPOINT ["/main"]
