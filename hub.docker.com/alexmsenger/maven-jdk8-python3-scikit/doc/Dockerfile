# Base Image
FROM alexiswl/containers:latest

# Metadata
LABEL base.image="biocontainers:latest"
LABEL version="1"
LABEL software="fastQC"
LABEL software.version="0.11.7"
LABEL description="FastQC is a QC tool for NGS data"
LABEL website="https://www.bioinformatics.babraham.ac.uk/projects/fastqc/"
LABEL documentation="https://www.bioinformatics.babraham.ac.uk/projects/fastqc/"
LABEL license="GPLv3"
LABEL tags="Genomics"

# Maintainer
MAINTAINER Alexis Lucattini <alexis.lucattini@agrf.org.au>

RUN conda install -c conda-forge perl=5.22.0
RUN conda install -c bioconda fastqc=0.11.7

WORKDIR /data/

ENTRYPOINT ["fastqc"]
