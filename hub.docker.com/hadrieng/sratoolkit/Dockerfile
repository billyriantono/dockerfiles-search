FROM hadrieng/docker_base

MAINTAINER Hadrien Gourlé <gourlehadrien@gmail.com>

# sratoolkit
RUN wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz && \
    tar zxfv sratoolkit.*-ubuntu64.tar.gz && \
    cp -r sratoolkit.*-ubuntu64/bin/* /usr/bin
