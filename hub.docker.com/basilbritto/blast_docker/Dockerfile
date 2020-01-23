FROM basilbritto/spades_docker
MAINTAINER Basil Britto <basilbritto.xavier@uantwerpen.be>

RUN apt-get update

# Blast+
RUN wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.7.1/ncbi-blast-2.7.1+-x64-linux.tar.gz && tar xf ncbi-blast-2.7.1+-x64-linux.tar.gz && rm ncbi-blast-2.7.1+-x64-linux.tar.gz

ENV PATH="/NGStools/ncbi-blast-2.7.1+/bin:${PATH}"
