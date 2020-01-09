FROM debian

WORKDIR /opt/pcengines

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-utils && \
    apt-get install -y git lsb-release simple-cdd xorriso

RUN git clone --depth 1 https://github.com/honzahommer/pcengines-apu-debian-cd.git . && \
    sed -i 's|^#\(d-i debian\-installer/allow_unauthenticated.*\)|\1|g' profiles/apu64.preseed && \
    sed -i 's|^d-i netcfg/get_hostname seen|#&|' profiles/apu64.preseed && \
    apt-get -y autoremove && \
    apt-get clean all && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME /opt/pcengines/images
VOLUME /opt/pcengines/profiles

ENTRYPOINT ["./build" ]
CMD ["apu64"]
