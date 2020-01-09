FROM biocontainers/biocontainers:latest

LABEL software="STAR"
LABEL software.version="2.5.4a"

RUN conda install -c bioconda star=2.5.4a

WORKDIR /data

CMD ["STAR"]