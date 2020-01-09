FROM golang:1.5
COPY . /go/src/webhook
WORKDIR /go/src/webhook
RUN go-wrapper download
RUN go-wrapper install
