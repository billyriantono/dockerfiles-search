FROM golang:1.13.4-alpine AS build
COPY . /usr/local/src
WORKDIR /usr/local/src
ENV GOOS linux
ENV GOARCH amd64
ENV CGO_ENABLED 0
RUN go build \
  -ldflags="-w -s" \
  -o /usr/local/bin/hello \
  main.go

FROM scratch
COPY --from=build /usr/local/bin/hello /
CMD ["/hello"]
