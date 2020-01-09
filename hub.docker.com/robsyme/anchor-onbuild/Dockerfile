FROM ubuntu

LABEL maintainer="Rob Syme <rob.syme@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -qqy && \
  apt-get install -y unzip zip wget libreadline-dev bc less nano \
  python python-numpy python-pandas python-matplotlib python-seaborn python-openpyxl python-biopython

WORKDIR /opt

# Mothur
RUN mkdir -p /opt/mothur && \
  cd /opt/mothur && \
  wget https://github.com/mothur/mothur/releases/download/v1.42.1/Mothur.linux_64_noReadline.zip && \
  unzip Mothur*.zip && \
  rm *.zip && \
  ln -s mothur current

# Blast
RUN mkdir -p /opt/blast && \
  cd /opt/blast && \
  wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/LATEST/ncbi-blast-2.9.0+-x64-linux.tar.gz && \
  tar -xvf ncbi-blast-*-linux.tar.gz && \
  rm ncbi-blast-*-linux.tar.gz && \
  ln -s ncbi-blast-* current

# usearch9
RUN mkdir -p /opt/usearch
ONBUILD ADD usearch9.2.64_i86linux32 /opt/usearch/usearch9
ONBUILD RUN rm /opt/anchor/current/pipelineScripts/usearch9/usearch9 && \
  ln -s /opt/usearch/usearch9 /opt/anchor/current/pipelineScripts/usearch9/usearch9

# Anchor
RUN mkdir -p /opt/anchor
ADD ANCHOR_v1.0 /opt/anchor/ANCHOR_v1.0
RUN ln -fs /opt/anchor/ANCHOR_v1.0 /opt/anchor/current && \
  ln -fs /opt/mothur/current/mothur /opt/anchor/current/pipelineScripts/mothur/mothur

ENV PATH "/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/mothur/current:/opt/blast/current/bin:/opt/usearch:/opt/anchor/current"
