#Use an official Ubuntu runtime as a parent image, which has already the subread aligner
FROM congelos/subread:latest

#MAINTAINER ConYel <https://github.com/ConYel>

# Set the working directory to /home
WORKDIR /home

#set User ROOT
USER root

RUN wget ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_32/GRCh38.primary_assembly.genome.fa.gz \ 
    && wget ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_32/gencode.v32.primary_assembly.annotation.gtf.gz \
    && mkdir hg38 && cd hg38  
  #  && subread-buildindex -o hg38 -F ../GRCh38.primary_assembly.genome.fa.gz \
  #  && rm ../GRCh38.primary_assembly.genome.fa.gz
    
