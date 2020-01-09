FROM golang:1.13-alpine AS builder
RUN mkdir /app
COPY . /app/
WORKDIR /app
RUN go get
RUN CGO_ENABLED=0 GOOS=linux go build -a -tags netgo -ldflags '-w' .
RUN echo "go:x:10001:10001::/:/bin/false" > passwd-file

FROM scratch
COPY --from=builder /app/passwd-file /etc/passwd
COPY --from=builder /app/ingress-enforcer .
USER go
EXPOSE 8443
CMD ["/ingress-enforcer"]
