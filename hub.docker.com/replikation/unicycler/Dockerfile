FROM ubuntu:bionic
ENV DEBIAN_FRONTEND=noninteractive
MAINTAINER Christian Brandt <christian.jena@gmail.com>

RUN apt-get update && apt-get install -y --no-install-recommends \
					 python3 \
					 python3-pip \
					 python3-setuptools \
           git \
           cmake \
					 make \
					 wget \
					 g++ \
           bzip2 \
           lbzip2 \
           libbz2-dev \
           zlib1g-dev \
           ncbi-blast+ \
           default-jre \
           liblzma-dev \
           unzip
RUN apt-get clean

RUN mkdir unicycler
WORKDIR unicycler

# Install SPAdes
RUN wget --no-check-certificate "http://cab.spbu.ru/files/release3.13.0/SPAdes-3.13.0.tar.gz" \
 		&& tar -xzf SPAdes-3.13.0.tar.gz \
 		&& mkdir -p /unicycler/SPAdes-3.13.0/src/build
WORKDIR /unicycler/SPAdes-3.13.0/src/build
RUN cmake ..
RUN make install
WORKDIR /unicycler
RUN rm -r SPAdes-3.13.0*

# Install racon
RUN git clone --recursive https://github.com/isovic/racon.git racon \
 		&& mkdir -p /unicycler/racon/build
WORKDIR /unicycler/racon/build
RUN cmake -DCMAKE_BUILD_TYPE=Release ..
RUN make && make install
WORKDIR /unicycler/
RUN rm -r racon*

# Install samtools
RUN wget --no-check-certificate https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2 \
		&& tar xjf samtools*.tar.bz2 ; rm samtools*.tar.bz2 \
		&& mv /unicycler/samtools-*/ /unicycler/samtools/
WORKDIR  /unicycler/samtools/
RUN ./configure --without-curses
RUN make && make install
WORKDIR /unicycler
RUN rm -r samtools*

# Install bowtie2
RUN wget --no-check-certificate https://github.com/BenLangmead/bowtie2/releases/download/v2.3.4.3/bowtie2-2.3.4.3-linux-x86_64.zip \
 		&& unzip bowtie2-*.zip \
 		&& mv /unicycler/bowtie2-*/ /unicycler/bowtie2/
WORKDIR /unicycler/bowtie2/
RUN mv bowtie2* /usr/local/bin
WORKDIR /unicycler
RUN rm -r bowtie2*
WORKDIR /

# Install Pilon
RUN cd /usr/local/bin/ && wget --no-check-certificate "https://github.com/broadinstitute/pilon/releases/download/v1.22/pilon-1.22.jar"

# Install minimap2
RUN git clone https://github.com/lh3/minimap2 \
 		&& cd minimap2 && make
ENV PATH /minimap2/:$PATH

# Install Unicycler
WORKDIR /unicycler
RUN git clone https://github.com/rrwick/Unicycler.git
WORKDIR /unicycler/Unicycler
ENV TERM=xterm
RUN python3 setup.py install
WORKDIR /unicycler
RUN rm -r Unicycler
WORKDIR /

# ENTRYPOINT
ENTRYPOINT ["unicycler"]
CMD ["--help"]

# clean up
RUN apt-get purge -y \
					 python3-pip \
					 python3-setuptools \
           git \
           cmake \
					 make \
					 wget
