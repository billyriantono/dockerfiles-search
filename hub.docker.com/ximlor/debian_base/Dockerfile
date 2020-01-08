FROM debian:stretch

# Modified to CST time zone
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ADD ./sources.list /etc/apt

RUN release=$(awk -F"[)(]+" '/VERSION=/ {print $2}' /etc/os-release) \
    && sed -i "s/{Release}/$release/" /etc/apt/sources.list \
    && apt-get -y update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends procps git curl wget \
    && DEBIAN_FRONTEND=noninteractive apt-get -y autoremove \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

