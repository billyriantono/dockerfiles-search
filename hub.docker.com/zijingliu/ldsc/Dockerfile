FROM continuumio/miniconda2:latest

RUN conda config --add channels bioconda && \
    conda install -y bitarray=0.8 && \
    conda install -y nose=1.3 && \
    conda install -y numpy=1.12 && \
    conda install -y pandas=0.20 && \
    conda install -y pybedtools=0.7 && \
    pip install scipy==0.18

RUN git clone https://github.com/bulik/ldsc.git

