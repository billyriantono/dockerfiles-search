FROM ubuntu:latest

RUN apt-get update && apt-get install -y wget \
    && wget -O kallisto-0.43.1.tar.gz https://github.com/pachterlab/kallisto/releases/download/v0.43.1/kallisto_linux-v0.43.1.tar.gz \
    && tar xvfz kallisto-0.43.1.tar.gz \
    && cp /kallisto_linux-v0.43.1/kallisto /usr/bin/kallisto \
    && rm -fr /kallisto_linux-v0.43.1/* \
    && rm -r /var/lib/apt/lists/*
