FROM hdf87ery/ubuntu_dev


LABEL maintainer="Shao-Min Wu" \
      contact="hdf87ery@hotmail.com"


# Define working directory.
RUN mkdir -p /apps
RUN mkdir -p /data
RUN mkdir -p /config
WORKDIR /apps  

# Install requirements
RUN pip install --upgrade pip && \
  pip install PyVCF ConfigParser Cheetah pysam numpy 
RUN pip install fisher


# install freebayes
RUN git clone --recursive git://github.com/ekg/freebayes.git && \
  cd freebayes && \
  make && \
  make install 

# install bam matcher
RUN apt-get install samtools  
RUN git clone https://bitbucket.org/sacgf/bam-matcher.git && \
  chmod a+x bam-matcher/bam-matcher.py

COPY 1kg.exome.highAF.7550.hg19.chr.vcf /apps/bam-matcher
COPY 1kg.exome.highAF.7550.hg38.chr.vcf /apps/bam-matcher
COPY bam-matcher.hg38.conf /config
COPY bam-matcher.hg19.conf /config

# ENV
ENV PATH="/apps/bam-matcher:${PATH}"

WORKDIR /data




