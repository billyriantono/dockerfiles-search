
FROM golang:alpine as builder

RUN mkdir /build && apk update && apk add --no-cache git
ADD . /build/
WORKDIR /build

RUN go get -d -v && GOOS=linux GOARCH=386 go build -o worker

FROM scratch

COPY --from=builder /build/worker /app/

WORKDIR /app

##EXPOSE 8080
CMD ["./worker"]
