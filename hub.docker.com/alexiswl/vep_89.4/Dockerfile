# Base Image
FROM alexiswl/containers:latest

# Metadata
LABEL base.image="biocontainers:latest"
LABEL version="1"
LABEL software="vep"
LABEL software.version="89"
LABEL description="variant effect predictor"
LABEL website="https://asia.ensembl.org/info/docs/tools/vep/index.html"
LABEL documentation="https://asia.ensembl.org/info/docs/tools/vep/script/vep_tutorial.html"
LABEL license="GPLv3"
LABEL tags="Genomics"

# Maintainer
MAINTAINER Alexis Lucattini <alexis.lucattini@agrf.org.au>

RUN conda install -c conda-forge perl=5.22.0 --yes
RUN conda install -c bioconda htslib=1.5.0 --yes
RUN conda install -c bioconda ensembl-vep=89.4 --yes

WORKDIR /data/

ENTRYPOINT ["vep"]
