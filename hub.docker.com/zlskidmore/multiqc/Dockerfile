# work from latest LTS ubuntu release
FROM ubuntu:18.04

# set environment variables
ENV multiqc_version 1.7
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# Install dependencies
RUN apt-get update -y && apt-get install -y \
    build-essential \
    libnss-sss \
    vim \
    wget \
    python3 \
    python3-pip \
    python3-yaml

# install kallisto
WORKDIR /usr/local/bin/
RUN wget https://github.com/ewels/MultiQC/archive/v${multiqc_version}.tar.gz
RUN tar -zxvf v${multiqc_version}.tar.gz
WORKDIR /usr/local/bin/MultiQC-${multiqc_version}
RUN python3 setup.py install

# set default command
CMD ["multiqc --help"]
