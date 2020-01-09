FROM golang as build

ENV GO111MODULE=on

WORKDIR /go/src/homee_exporter
COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

FROM gcr.io/distroless/base
COPY --from=build /go/bin/homee_exporter /
CMD ["/homee_exporter"]