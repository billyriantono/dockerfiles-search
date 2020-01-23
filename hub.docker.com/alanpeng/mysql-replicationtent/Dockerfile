FROM alaindomissy/docker-biopython
MAINTAINER Alain Domissy alaindomissy@gmail.com

RUN conda install -y \
  cython==0.23.4 \
  pandas=0.18.1 \
  scipy=0.17.1


RUN conda install -c johanneskoester bcftools
RUN conda install -c bioconda pysam

#RUN conda install -c r ncurses
#RUN pip install pysam==0.8

# root development executables
# app executables
ENV PATH /opt/blast/bin:/root/bin:$PATH

COPY files /root/bin

#WORKDIR /root/

#RUN apt-get install nano tree

#CMD /BACKEND/appgithub.sh
