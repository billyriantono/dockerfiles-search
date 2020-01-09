FROM ubuntu:latest

RUN apt-get update && apt-get install -y wget \
    && wget -O salmon-0.11.3-linux_x86_64.tar.gz https://github.com/COMBINE-lab/salmon/releases/download/v0.11.3/salmon-0.11.3-linux_x86_64.tar.gz \
    && tar xvfz salmon-0.11.3-linux_x86_64.tar.gz \
    && cp /salmon-0.11.3-linux_x86_64/bin/salmon /usr/bin/salmon \
    && cp -r /salmon-0.11.3-linux_x86_64/lib/* /usr/bin \
    && rm -r /var/lib/apt/lists/*
