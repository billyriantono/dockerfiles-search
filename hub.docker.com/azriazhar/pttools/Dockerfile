FROM loadimpact/k6 as k6
FROM alpine:edge
RUN apk update;apk add nghttp2;apk add iperf3; apk add curl; apk add tcpdump
COPY --from=k6 /usr/bin/k6 /usr/bin/k6
CMD ["/bin/sh"]
