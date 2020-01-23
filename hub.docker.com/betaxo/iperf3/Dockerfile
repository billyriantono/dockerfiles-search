FROM alpine:latest

RUN apk add --no-cache iperf3

EXPOSE 5201/tcp 5201/udp

ENTRYPOINT ["iperf3"]

# iperf3 -s = run in Server mode
CMD ["-s"]
