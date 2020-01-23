FROM golang:latest as builder
RUN CGO_ENABLED=0 GOOS=linux go install -a -installsuffix=nocgo std
WORKDIR /project
COPY go.sum go.mod ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-s -w" -installsuffix=nocgo -o=/tmp/leproxy

FROM scratch
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=builder /tmp/leproxy .
VOLUME /data
EXPOSE 80
EXPOSE 443
ENTRYPOINT ["./leproxy", "-http=:80", "-addr=:443"]
