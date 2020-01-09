# Base Image
FROM alexiswl/containers:latest

# Metadata
LABEL base.image="biocontainers:latest"
LABEL version="1"
LABEL software="star"
LABEL software.version="2.5.3a"
LABEL description="Spliced Transcripts Alignment to a Reference"
LABEL website="https://github.com/alexdobin/STAR"
LABEL documentation="https://github.com/alexdobin/STAR"
LABEL license="https://github.com/alexdobin/STAR"
LABEL tags="Genomics"

# Maintainer
MAINTAINER Alexis Lucattini <alexis.lucattini@agrf.org.au>

RUN conda install -c bioconda star=2.5.3a

WORKDIR /data/

ENTRYPOINT ["STAR"]
