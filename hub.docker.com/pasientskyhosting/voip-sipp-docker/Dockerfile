
FROM debian:jessie

MAINTAINER Karsten Kaj Jakobsen <kj@patientsky.com>
ENV SIPP_VERSION 3.6.0

RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential curl automake ncurses-dev libssl-dev libsctp-dev libpcap-dev git ca-certificates pkg-config && \
    rm -rf /var/lib/apt/lists/*

# curl -sqLkv https://github.com/SIPp/sipp/releases/download/v${SIPP_VERSION}/sipp-${SIPP_VERSION}.tar.gz | tar xvzf - --strip-components=1 && \

RUN mkdir /build /data && \
    chmod 775 /build && \
    cd /build

RUN git clone https://github.com/SIPp/sipp && \
    cd sipp && \
    ./build.sh --with-openssl --with-pcap --with-rtpstream --with-sctp && \
    mv sipp /usr/bin

RUN apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

# Create sipp scenarios, artifacts and audio
RUN mkdir -p /var/lib/sipp/scenarios
RUN mkdir -p /var/lib/sipp/audio
RUN mkdir -p /var/lib/sipp/artifacts

COPY audio/ /var/lib/sipp/audio/

# Copy our entrypoint file
COPY entrypoint.sh /

RUN chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]
