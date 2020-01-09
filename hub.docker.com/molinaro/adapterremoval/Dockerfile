ARG     BASE_CONTAINER=continuumio/miniconda3

FROM    $BASE_CONTAINER

MAINTAINER Emiliano Molinaro <molinaro@imada.sdu.dk>

LABEL   authors="Mikkel Schubert <MikkelSch@gmail.com> and Stinus Lindgreen <stinus@binf.ku.dk>" \
		version="2.2.2" \
        description="This program searches for and removes remnant adapter sequences from High-Throughput Sequencing (HTS) data and (optionally) trims low quality bases from the 3' end of reads following adapter removal. AdapterRemoval can analyze both single end and paired end data, and can be used to merge overlapping paired-ended reads into (longer) consensus sequences. Additionally, the AdapterRemoval may be used to recover a consensus adapter sequence for paired-ended data, for which this information is not available"

RUN     apt-get update && apt-get install -y build-essential && rm -rf /var/lib/apt/lists/* 

COPY 	environment.yml /
RUN 	conda env create -f /environment.yml && conda clean -a
ENV 	PATH /opt/conda/envs/adapterremoval2/bin:$PATH