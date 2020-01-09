FROM golang:1.5
COPY . /go/src/mailhook
WORKDIR /go/src/mailhook
RUN go-wrapper download
RUN go-wrapper install
