FROM debian:stretch-slim as builder
ENV NDPPD_VERSION 0.2.5
RUN apt update && \
    apt install -y --no-install-recommends \
        ca-certificates \
        make \
        g++ \
        curl && \
    curl -LO https://github.com/DanielAdolfsson/ndppd/archive/${NDPPD_VERSION}.tar.gz && \
    tar xzvf ${NDPPD_VERSION}.tar.gz -C /usr/local/src && \
    cd /usr/local/src/ndppd-${NDPPD_VERSION} && \
    make all && \
    make install

FROM debian:stretch-slim
COPY --from=builder /usr/local/sbin/ndppd /usr/local/sbin/ndppd
RUN mkdir /etc/ndppd
CMD ["/usr/local/sbin/ndppd -c /etc/ndppd/ndppd.conf"]