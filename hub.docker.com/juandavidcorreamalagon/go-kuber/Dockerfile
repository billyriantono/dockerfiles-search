#------
FROM golang:latest as govendor

WORKDIR /go/src/app

RUN go get -u github.com/kardianos/govendor

COPY . .

RUN go build

#------

FROM golang:1.8

WORKDIR /go/src/app

COPY --from=govendor /go/src/app/app .

#ENV PORT 8082

CMD ["./app"]