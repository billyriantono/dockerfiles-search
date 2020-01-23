FROM golang:1.13

WORKDIR /go/src/github.com/brynelee/xdsimplego
COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

CMD ["xdsimplego"]

EXPOSE 8080

