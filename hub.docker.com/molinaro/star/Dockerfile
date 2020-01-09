ARG     BASE_CONTAINER=continuumio/miniconda3

FROM    $BASE_CONTAINER

MAINTAINER Emiliano Molinaro <molinaro@imada.sdu.dk>

LABEL   author="Alexander Dobin <dobin@cshl.edu>" \
		versions="2.5.4a" \
		description="Spliced Transcripts Alignment to a Reference" 

RUN     apt-get update && apt-get install -y build-essential && rm -rf /var/lib/apt/lists/* 

COPY 	environment.yml /
RUN 	conda env create -f /environment.yml && conda clean -a
ENV 	PATH /opt/conda/envs/star/bin:$PATH
