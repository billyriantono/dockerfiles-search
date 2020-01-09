FROM ubuntu
MAINTAINER Nuno Agostinho <nunodanielagostinho@gmail.com>

RUN apt-get update

# Install sra-toolkit
WORKDIR /NGStools/
RUN apt-get install -y wget
RUN wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.8.2-1/sratoolkit.2.8.2-1-ubuntu64.tar.gz
RUN tar -zxvf sratoolkit.2.8.2-1-ubuntu64.tar.gz
RUN rm sratoolkit.2.8.2-1-ubuntu64.tar.gz
ENV PATH="/NGStools/sratoolkit.2.8.2-1-ubuntu64/bin:${PATH}"

# Install parallel-fastq-dump
COPY get-pip.py .
RUN apt-get install -y python3 python3-distutils
RUN python3 get-pip.py
RUN rm get-pip.py

RUN pip3 install --upgrade pip
RUN pip3 install parallel-fastq-dump
