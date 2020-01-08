FROM r-base:3.4.3

RUN apt-get update && \
    apt-get install -y wget libc6 libxml2-dev libcurl4-openssl-dev libssl-dev

RUN cd /opt \
    && wget https://github.com/nghiavtr/FuSeq/releases/download/v1.1.1/FuSeq_v1.1.1_linux_x86-64.tar.gz -O FuSeq_v1.1.1_linux_x86-64.tar.gz \
    && tar -xzvf FuSeq_v1.1.1_linux_x86-64.tar.gz \
    && cd FuSeq_v1.1.1_linux_x86-64 \
    && bash configure.sh \
    && rm linux/lib/librt.so.1

RUN R -e 'install.packages("stringi");source("https://bioconductor.org/biocLite.R");biocLite();biocLite(pkgs=c("GenomicFeatures"))'

ENV FUSEQ_HOME /opt/FuSeq_v1.1.1_linux_x86-64
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:$FUSEQ_HOME/linux/lib
ENV PATH $PATH:$FUSEQ_HOME/linux/bin

WORKDIR /home

# create volumes for MSK users
VOLUME ["/data", "/gpfs", "/ifs"]
