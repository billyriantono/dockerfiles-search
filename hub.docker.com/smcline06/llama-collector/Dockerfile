FROM golang:1.13.3

WORKDIR /go/src/app

copy config.yaml config.yaml

RUN go get -d -v github.com/dropbox/llama
RUN go install -v github.com/dropbox/llama/cmd/collector

# Port the reflector is listening on, 8100 is default
ENV DST_PORT=8100

CMD ["sh", "-c", "collector -llama.config config.yaml -llama.dst-port $DST_PORT"]
