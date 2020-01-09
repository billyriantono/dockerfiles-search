FROM ubuntu:latest
RUN apt-get update && apt-get -y upgrade \
    && apt-get -y install wget \
    && wget -O kallisto-0.44.0.tar.gz https://github.com/pachterlab/kallisto/releases/download/v0.44.0/kallisto_linux-v0.44.0.tar.gz \
    && tar xvfz kallisto-0.44.0.tar.gz \
    && cd kallisto_linux-v0.44.0 \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

ENV PATH $PATH:/kallisto_linux-v0.44.0
RUN echo $PATH
WORKDIR /kallisto_linux-v0.44.0
