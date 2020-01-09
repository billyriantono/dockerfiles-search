FROM ubuntu:18.04 as builder
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update \
    && apt install -y \
        gcc \
        make \
        bison \
        flex \
        m4 \
        libncurses5-dev \
        libreadline-dev \
        curl \
        autoconf \
        tar \
    && curl -LO https://github.com/BIRD/bird/archive/v2.0.2.tar.gz \
    && tar xzvf v2.0.2.tar.gz \
    && cd bird-2.0.2 \
    && autoreconf \
    && ./configure \
    && make \
    && make install \
    && cd .. ; rm -rf bird-2.0.2 v2.0.2.tar.gz \
    && apt clean autoclean \
    && apt autoremove -y \
    && rm -rf /var/lib/{apt,dpkg,cache,log}

FROM ubuntu:18.04
ENV DEBIAN_FRONTEND=noninteractive
COPY --from=builder /usr/local/sbin/* /usr/local/sbin/
COPY --from=builder /lib/x86_64-linux-gnu/libreadline.so.7 /usr/local/lib/
RUN mkdir -p /etc/bird /usr/local/var/run \
    && ldconfig

CMD ["bird", "-d", "-c", "/etc/bird/bird.conf"]
