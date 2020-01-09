ARG     BASE_CONTAINER=continuumio/miniconda3

FROM    $BASE_CONTAINER

MAINTAINER Emiliano Molinaro <molinaro@imada.sdu.dk>

LABEL   author="Chris Benner" \
		version="4.9.1" \
		description="HOMER (Hypergeometric Optimization of Motif EnRichment) is a suite of tools for Motif Discovery and next-gen sequencing analysis.  It is a collection of command line programs for unix-style operating systems written in Perl and C++. HOMER was primarily written as a de novo motif discovery algorithm and is well suited for finding 8-20 bp motifs in large scale genomics data.  HOMER contains many useful tools for analyzing ChIP-Seq, GRO-Seq, RNA-Seq, DNase-Seq, Hi-C and numerous other types of functional genomics sequencing data sets"

RUN     apt-get update && apt-get install -y build-essential && rm -rf /var/lib/apt/lists/*  

COPY 	environment.yml /
RUN 	conda env create -f /environment.yml && conda clean -a
ENV 	PATH /opt/conda/envs/homer/bin:$PATH