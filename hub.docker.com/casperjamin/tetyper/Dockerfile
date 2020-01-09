
FROM ubuntu:16.04

run apt-get update && apt-get -y install \
    wget \
    make \
    gcc

	


# lets get miniconda to do installs
RUN wget  --no-check-certificate https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh  
RUN chmod +x Miniconda3-latest-Linux-x86_64.sh   
RUN bash Miniconda3-latest-Linux-x86_64.sh -b -p /usr/miniconda3
ENV PATH /usr/miniconda3/bin:$PATH
RUN conda config --add channels r
RUN conda config --add channels conda-forge
RUN conda config --add channels bioconda

#install SPAdes
RUN conda install spades --yes

#install samtools
RUN conda install samtools --yes

#install bcftools
run conda install bcftools --yes

#install Blast
run conda install blast --yes

#install pysam via conda, less headaches via the pip install
RUN conda install -c bioconda pysam

run conda install -c bioconda bwa

#install TETyper

RUN pip install --upgrade pip


RUN pip install TETyper







