FROM debian

RUN mkdir -p /output
WORKDIR /output

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    gawk \
    curl \
    libav-tools \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

COPY . /usr/src/app/
ENTRYPOINT ["/usr/src/app/nrk-tv-downloader.sh"]
