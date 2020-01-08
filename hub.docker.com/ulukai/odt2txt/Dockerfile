FROM ubuntu

RUN apt-get update \
    && apt-get install -y --no-install-recommends odt2txt \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /root

ENTRYPOINT ["odt2txt"]
