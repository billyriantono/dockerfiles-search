FROM continuumio/miniconda

RUN conda install -c bioconda genenotebook=0.1.16

COPY ./wait-for-it/wait-for-it.sh /bin

EXPOSE 3000

CMD ["genenotebook","run"]