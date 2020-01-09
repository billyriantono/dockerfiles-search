FROM ubuntu:xenial

# Ubuntu Packages
RUN apt-get update && \
    apt-get install -y wget gawk gcc g++ make cmake automake curl unzip zip bzip2 \
    tar gzip pigz parallel build-essential libncurses5-dev libc6-dev zlib1g zlib1g-dev \
    libtbb-dev libtbb2 python python-dev python-numpy python-biopython python-xlrd \
    python-openpyxl default-jdk

# FusionCatcher
RUN cd /opt && \
    wget https://sourceforge.net/projects/fusioncatcher/files/fusioncatcher_v1.00.zip/download \
    -O fusioncatcher_v1.00.zip && \
    unzip fusioncatcher_v1.00.zip && rm fusioncatcher_v1.00.zip && \
    python fusioncatcher_v1.00/bin/bootstrap.py -x -y -i fusioncatcher_v1.00 && \
    rm fusioncatcher_v1.00/fusioncatcher_v1.00.zip

ENV PATH $PATH:/opt/fusioncatcher_v1.00/bin
ENV PATH $PATH:/opt/fusioncatcher_v1.00/tools/samtools

WORKDIR /home

# create volumes for MSK users
VOLUME ["/data", "/gpfs", "/ifs"]

ENTRYPOINT [ "fusioncatcher" ]
