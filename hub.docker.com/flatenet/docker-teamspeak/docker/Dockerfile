FROM continuumio/miniconda3:latest
MAINTAINER Fabian Kloosterman <kloosterman.nerf@gmail.com>

#RUN apt-get update --fix-missing && \
#    apt-get install -y g++ && \
#    apt-get clean && \
#    rm -rf /var/lib/apt/lists/*

RUN conda update conda && \
    conda install conda-build anaconda-client && \
    conda config --append channels conda-forge && \
    conda config --append channels KloostermanLab

CMD [ "/bin/bash" ]
