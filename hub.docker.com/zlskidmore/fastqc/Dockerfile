# work from latest LTS ubuntu release
FROM ubuntu:18.04

# set the environment variables
ENV fastqc_version 0.11.8

# run update and install necessary tools
RUN apt-get update -y && apt-get install -y \
    build-essential \
    libnss-sss \
    openjdk-8-jdk \
    curl \
    vim \
    less \
    wget \
    unzip

# install fastqc
WORKDIR /usr/local/bin/
RUN wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v${fastqc_version}.zip
RUN unzip fastqc_v${fastqc_version}.zip
WORKDIR /usr/local/bin/FastQC/
RUN chmod 755 fastqc
RUN ln -s /usr/local/bin/FastQC/fastqc /usr/local/bin/fastqc
WORKDIR /usr/local/bin

# set default command
CMD ["fastqc --help"]
