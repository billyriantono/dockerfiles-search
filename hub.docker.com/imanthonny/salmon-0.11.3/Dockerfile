FROM ubuntu:latest
RUN apt-get update && apt-get -y upgrade \
    && apt-get -y install wget \
    && wget -O salmon-0.11.3-linux_x86_64.tar.gz https://github.com/COMBINE-lab/salmon/releases/download/v0.11.3/salmon-0.11.3-linux_x86_64.tar.gz \
    && tar xvfz salmon-0.11.3-linux_x86_64.tar.gz \
    && cd salmon-0.11.3-linux_x86_64 \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

ENV PATH $PATH:/salmon-0.11.3-linux_x86_64/bin
RUN echo $PATH
WORKDIR /salmon-0.11.3-linux_x86_64
