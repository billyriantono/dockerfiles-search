FROM alpine:latest AS builder
COPY . /root/tinyblog/
WORKDIR /root/tinyblog
ENV GO111MODULE on
ENV GOPROXY https://goproxy.io
RUN apk update && apk add zip go make ca-certificates git musl-dev
RUN make pack

FROM alpine:latest
WORKDIR /app/
COPY --from=builder /root/tinyblog/pack/ ./
COPY --from=builder /root/tinyblog/docker-startup.sh .
RUN apk add --no-cache tzdata
RUN chmod +x docker-startup.sh
CMD ["./docker-startup.sh"]
