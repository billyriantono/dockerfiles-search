FROM golang AS build
WORKDIR /go/src/github.com/mashi6p/google-wire-hands-on/
RUN go get github.com/google/wire/cmd/wire
COPY . .
RUN go get -d -v ./... && \
    wire && \
    go build -o app

FROM alpine
RUN apk --no-cache add ca-certificates
WORKDIR /app
COPY --from=build /go/src/github.com/mashi6p/google-wire-hands-on/app .
CMD ["./app"]