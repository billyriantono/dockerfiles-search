FROM golang:1.12 as build

LABEL repository="https://github.com/pjbgf/zaz/"

WORKDIR /go/src/pjbgf/zaz
ADD . /go/src/pjbgf/zaz

ENV GO111MODULE=on

COPY go.mod go.mod
COPY go.sum go.sum
RUN go mod download

RUN go get -d -v ./...

RUN go build -o /go/bin/zaz

FROM gcr.io/distroless/base
COPY --from=build /go/bin/zaz /
CMD ["/zaz"]