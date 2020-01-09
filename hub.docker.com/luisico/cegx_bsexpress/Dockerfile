FROM ubuntu:16.04

# Install build dependencies, bedtools and r-base
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget tar unzip git python-pip python-setuptools \
    python-dev make build-essential libssl-dev zlib1g zlib1g-dev ncurses-dev \
    openjdk-8-jre \
    bedtools r-base \
 && rm -rf /var/lib/apt/lists/*

# Install samtools
RUN wget http://sourceforge.net/projects/samtools/files/samtools/1.1/samtools-1.1.tar.bz2/download -O - | tar --no-same-owner -xjf - -C /tmp \
 && cd /tmp/samtools-1.1 \
 && make install \
 && rm -rf /tmp/samtools-1.1

# Install bowtie
RUN wget http://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.2.6/bowtie2-2.2.6-linux-x86_64.zip -O /tmp/bowtie2-2.2.6-linux-x86_64.zip \
 && unzip -d /tmp /tmp/bowtie2-2.2.6-linux-x86_64.zip \
 && cp /tmp/bowtie2-2.2.6/bowtie2* /usr/local/bin/ \
 && rm -rf /tmp/bowtie2-2.2.6-linux-x86_64.zip /tmp/bowtie2-2.2.6

# Install cutadapt
RUN pip --no-cache-dir install --upgrade cutadapt

# Install bamutils
RUN wget http://genome.sph.umich.edu/w/images/7/70/BamUtilLibStatGen.1.0.13.tgz -O - | tar --no-same-owner -xzf - -C /tmp \
 && cd /tmp/bamUtil_1.0.13 \
 && rm -rf libStatGen \
 && git clone https://github.com/statgen/libStatGen.git \
 && make install \
 && rm -rf /tmp/bamUtil_1.0.13

# Install cegx_bsexpress
COPY . /cegx_bsexpress/

RUN cd /cegx_bsexpress \
 && sed -i'' -e "/if encoding == 'Sanger':/,+13 s/^/#/" /cegx_bsexpress/oxbs_qc/oxbs_qc_func.py \
 && sed -i'' -e "s/^\(bdg = bdg\[!(bdg\$chrom == 'SQfC'),\]\)/# \1/" /cegx_bsexpress/oxbs_qc/oxbs_report.R \
 && python setup.py install --install-scripts /usr/local/bin

# Signal we are in a container
ENV INCONTAINER=docker

# Change working directory
WORKDIR /Data

# Start auto_bsExpress without options
ENTRYPOINT ["auto_bsExpress"]
