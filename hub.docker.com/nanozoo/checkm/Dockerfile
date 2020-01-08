FROM continuumio/miniconda3
ENV VERSION 1.0.13

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda config --add channels conda-forge && \
    conda config --add channels bioconda && \
    conda config --add channels default

RUN conda install python=2.7 checkm-genome=$VERSION && conda clean -a

# database setup
RUN wget --no-check-certificate https://data.ace.uq.edu.au/public/CheckM_databases/checkm_data_2015_01_16.tar.gz && \
        mkdir -p /checkm_database \
		&& tar -xzf checkm_data_2015_01_16.tar.gz -C /checkm_database \
		&& rm -rf checkm_data_2015_01_16.tar.gz
RUN echo /checkm_database | checkm data setRoot /checkm_database
