FROM continuumio/miniconda3:4.5.4

RUN conda config --add channels defaults
RUN conda config --add channels conda-forge
RUN conda config --add channels bioconda

RUN conda install -y star multiqc trim-galore subread fastqc gatk
