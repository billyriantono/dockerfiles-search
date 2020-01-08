FROM continuumio/miniconda3
ENV VERSION 0.10.0

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda config --add channels conda-forge && \
		conda config --add channels bioconda && \
		conda config --add channels default

RUN conda install python=3.6 medaka=$VERSION && conda clean -a

# hack for samtools lib issue (wrong conda recipe)
RUN cd /opt/conda/lib && ln -s libcrypto.so.1.1 libcrypto.so.1.0.0
