FROM ubuntu:16.04
MAINTAINER Yongqi WANG <yongqi.wang.cn@gmail.com>

# The archive software SOFTWARE_NAME are downloaded into the dir
# /tmp/SOFTWARE_NAME/, decompressed and move to /tools/
# Other executable software are directly downloaded to dir 
# /tools/SOFTWARE_NAME/
# Create a symbolic linke in the $PATH by the following command
# ln -s /tools/SOFTWARE_NAME/EXE /usr/local/bin/EXE
# Granting access to certain users is still unclear

# Dockerfile: ngs-pipeline:ngs-pipeline

#---------------------------------------------------------------------
# PRE-INSTALLATION
#---------------------------------------------------------------------

# Install python and dependencies, as well
# as a few extras for helpful debugging and testing.
# Install default-jre for fastqc

RUN apt-get update && \
    apt-get install -y --force-yes \
    git \
    default-jre \
    libffi-dev \
    libssl-dev \
    make \
    parallel \
    python \
    python-dev \
    python-numpy \
    python-distribute \
    python-pip \
    unzip \
    wget 

# Create the folder for all the tools needed
RUN mkdir -p /tools

# Install the required Python packages. May also install these via requirements.txt
RUN pip install --upgrade pip

#---------------------------------------------------------------------
# !A: NCBI PROGRAM
#---------------------------------------------------------------------

# Install software: twoBitToFa
# Install the dependecies for twoBitToFa: libpng12-0
# Install the local .deb package using apt
# Execute bit for everyone with flag +x

RUN wget -O /tmp/libpng12-0_1.2.54-1ubuntu1_amd64.deb http://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb && \
    apt install /tmp/libpng12-0_1.2.54-1ubuntu1_amd64.deb && \
    mkdir -p /tools/twoBitToFa/ && \ 
    wget -O /tools/twoBitToFa/twoBitToFa http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/twoBitToFa && \ 
    chmod +x /tools/twoBitToFa/twoBitToFa && \
    ln -s /tools/twoBitToFa/twoBitToFa /usr/local/bin/twoBitToFa

# Install software: SRA toolkit
#RUN mkdir -p /tools/sratoolkit && \
#    wget -O /tmp/sratoolkit.tar.gz http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz && \
#    tar xvzf /tmp/sratoolkit.tar.gz -C /tools/sratoolkit/ && \
#    cd /tools/sratoolkit/ && \
#    PATH=$PATH:$PWD/sratoolkit.2.8.2-1-ubuntu64/bin
RUN apt-get install -y --force-yes sra-toolkit

#---------------------------------------------------------------------
# !B: QUALITY CONTROL
#---------------------------------------------------------------------

# Install software: FastQC 

RUN wget -O /tmp/fastqc_v0.11.5.zip http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip && \
    unzip /tmp/fastqc_*.zip -d /tools/ && \
    chmod +x /tools/FastQC/fastqc && \
    ln -s /tools/FastQC/fastqc /usr/local/bin/fastqc 

# Install software: MultiQC
RUN pip install multiqc

#---------------------------------------------------------------------
# !C: ALIGNMENT SOFTWARE
#---------------------------------------------------------------------

# Install software: Teaser
# link (https://github.com/Cibiv/Teaser/blob/master/Dockerfile)
RUN apt-get install -y --force-yes \
    zlib1g-dev \
    cmake && \ 
    pip install intervaltree tornado pyaml psutil numpy
RUN echo "#!/bin/bash" > /usr/bin/teaser_shell.sh; echo "cd /teaser; python install.py 2> /dev/null; mv install.py _install.py 2> /dev/null;  bash" >> /usr/bin/teaser_shell.sh; chmod +x /usr/bin/teaser_shell.sh; ln -s /teaser/teaser.py /usr/bin/teaser; ln -s /teaser/teaser.py /usr/bin/teaser.py;

# Install software: BWA
RUN mkdir -p /tools/bwa/ && \
    wget -O /tmp/bwa-0.7.15.tar.bz2 https://sourceforge.net/projects/bio-bwa/files/bwa-0.7.15.tar.bz2/download && \
    tar xjf /tmp/bwa-0.7.15.tar.bz2 -C /tools/bwa/ && \
    cd /tools/bwa/bwa-0.7.15/ && \
    make && \
    ln -s /tools/bwa/bwa-0.7.15/bwa /usr/local/bin/bwa

# Install software: Bowtie
RUN apt-get install -y --force-yes \
    bowtie

# Install software: Bowtie2
RUN apt-get install -y --force-yes \
    libtbb2 \
    bowtie2  

#---------------------------------------------------------------------
# !D: OTHER
#---------------------------------------------------------------------

# Install software: samtools
RUN apt-get install -y --force-yes samtools 

# Install software: bedtools
RUN apt-get install -y --force-yes bedtools

# Install software: deepTools
RUN git clone https://github.com/fidelram/deepTools && \
    cd deepTools && \
    python setup.py install

# Install software: samblaster
RUN git clone git://github.com/GregoryFaust/samblaster.git && \
    cd samblaster && \
    make && \
    cp samblaster /usr/local/bin/.

# Install Aspera Command-Line Interface
RUN wget http://download.asperasoft.com/download/sw/cli/3.7.2/aspera-cli-3.7.2.354.010c3b8-linux-64-release.sh && \
    chmod +x aspera-cli*sh && \
    export PATH=~/.aspera/cli/bin:\$PATH

#---------------------------------------------------------------------
# !E: PEAK CALLING
#---------------------------------------------------------------------

# Install software: MACS2
RUN pip install MACS2

#---------------------------------------------------------------------
# !F: R and bioconductor (No idea how~~~)
#---------------------------------------------------------------------

# Install software: R and its dependenies
RUN apt-get install -y --force-yes \
    r-base-dev \
    r-base \
    r-base-dev


#---------------------------------------------------------------------
# POST-INSTALLATION
#---------------------------------------------------------------------

# Clean-up
RUN apt-get clean && \
    rm -rf /tmp/*