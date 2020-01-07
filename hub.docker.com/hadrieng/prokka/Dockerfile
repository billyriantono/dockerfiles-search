FROM hadrieng/docker_base

MAINTAINER Hadrien Gourlé <gourlehadrien@gmail.com>

# install perl deps mummer python3 and java
RUN apt-get install -y libdatetime-perl \
    libxml-simple-perl libdigest-md5-perl bioperl \
    mummer python3 python3-dev libxml2-dev libxslt-dev \
    python-genometools genometools python-dev python-setuptools \
    default-jre

# install prokka
RUN git clone https://github.com/tseemann/prokka.git && \
    prokka/bin/prokka --setupdb

# install newer tbl2asn
RUN wget ftp://ftp.ncbi.nih.gov/toolbox/ncbi_tools/converters/by_program/tbl2asn/linux64.tbl2asn.gz && \
    gzip -d linux64.tbl2asn.gz && \
    chmod 755 linux64.tbl2asn && \
    mv linux64.tbl2asn /prokka/binaries/linux/tbl2asn

# add prokka and prodigal to path
ENV PATH /prokka/bin:/prokka/binaries/linux:$PATH

# install bwa
RUN wget https://github.com/lh3/bwa/releases/download/v0.7.15/bwa-0.7.15.tar.bz2 && \
    tar xf bwa-0.7.15.tar.bz2 && \
    cd bwa-0.7.15 && \
    make

# add bwa to path
ENV PATH /bwa-0.7.15:$PATH

# install spades
RUN wget http://cab.spbu.ru/files/release3.9.1/SPAdes-3.9.1-Linux.tar.gz && \
    tar xzf SPAdes-3.9.1-Linux.tar.gz

# add spades to path
ENV PATH /SPAdes-3.9.1-Linux/bin:$PATH

# install circlator
RUN wget https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    pip3 install circlator

# install gff3toembl
RUN wget https://github.com/sanger-pathogens/gff3toembl/archive/v1.1.4.tar.gz && \
    tar xzf v1.1.4.tar.gz && \
    rm v1.1.4.tar.gz && \
    cd gff3toembl-1.1.4 && \
    python setup.py install && \
    ln -s /usr/lib/libgenometools.so.0 /usr/lib/libgenometools.so
