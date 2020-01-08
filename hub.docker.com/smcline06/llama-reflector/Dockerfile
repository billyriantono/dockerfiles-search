FROM golang:1.13.3

WORKDIR /go/src/app

RUN go get -d -v github.com/dropbox/llama
RUN go install -v github.com/dropbox/llama/cmd/reflector

# Listening Port, 8100 is default
ENV PORT=8100

CMD ["sh", "-c", "reflector -port $PORT"]
