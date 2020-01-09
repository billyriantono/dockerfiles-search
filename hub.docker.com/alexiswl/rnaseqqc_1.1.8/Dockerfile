# Base Image
FROM alexiswl/containers:latest

# Metadata
LABEL base.image="biocontainers:latest"
LABEL version="1"
LABEL software="RNA-SeQC"
LABEL software.version="1.1.8"
LABEL description="RNA-SeQC is a java program which computes a series of quality control metrics for RNA-seq data."
LABEL website="http://archive.broadinstitute.org/cancer/cga/rna-seqc"
LABEL documentation="http://archive.broadinstitute.org/cancer/cga/rnaseqc_run"
LABEL license="GPLv3"
LABEL tags="Genomics"

# Maintainer
MAINTAINER Alexis Lucattini <alexis.lucattini@agrf.org.au>

# Install perl, bwa and rnaseqc
RUN conda install -c conda-forge perl=5.22.0
RUN conda install -c bioconda bwa=0.7.16
# Requires Java 1.7 not 1.8. 
RUN conda install -c bioconda java-jdk=7.0.91
# Install without upgrading to Java1.8
RUN conda install -c bioconda --no-deps rna-seqc=1.1.8

WORKDIR /data/

ENTRYPOINT ["rna-seqc"]
