FROM ubuntu:latest


RUN apt-get install -f
RUN apt-get update
RUN apt-get install -y openjdk-8-jdk

RUN apt-get update && apt-get -y upgrade \
    && apt-get update -y && apt-get install -y wget unzip \
    && wget "https://github.com/broadinstitute/picard/releases/download/2.17.2/picard.jar" \
    && mv /picard.jar /usr/bin

RUN apt-get update && apt-get install -y wget \
    && wget -O kallisto-0.44.0.tar.gz https://github.com/pachterlab/kallisto/releases/download/v0.44.0/kallisto_linux-v0.44.0.tar.gz \
    && tar xvfz kallisto-0.44.0.tar.gz \
    && cp /kallisto_linux-v0.44.0/kallisto /usr/bin/kallisto \
    && rm -fr /kallisto_linux-v0.44.0/* \
    && rm -r /var/lib/apt/lists/*
