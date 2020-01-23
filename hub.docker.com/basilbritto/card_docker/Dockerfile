FROM basilbritto/parsnp_docker
MAINTAINER Basil Britto <basilbritto.xavier@uantwerpen.be>

WORKDIR /NGStools/card

RUN wget https://card.mcmaster.ca/download/6/prevalence-v3.0.1.tar.gz
RUN tar -xvf prevalence-v3.0.1.tar.gz
RUN rm prevalence-v3.0.1.tar.gz

RUN mkdir nucleotide protein
RUN mv protein_* protein/
RUN mv nucleotide_* nucleotide/
