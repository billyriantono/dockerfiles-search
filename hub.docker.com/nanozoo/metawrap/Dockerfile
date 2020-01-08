FROM continuumio/miniconda3
ENV VERSION 1.2.2 

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda config --add channels conda-forge && \
    conda config --add channels bioconda && \
    conda config --add channels default

RUN conda install python=2.7 biopython checkm-genome  
# maxbin2 megahit metabat2 spades blas=2.5 samtools=1.9  salmon blast=2.6.0 bmtagger bowtie2 bwa matplotlib quast r-ggplot2 pandas prokka  r-recommended seaborn  trim-galore

RUN git clone https://github.com/bxlab/metaWRAP
ENV PATH /metaWRAP/bin/:$PATH

# database setup
RUN wget --no-check-certificate https://data.ace.uq.edu.au/public/CheckM_databases/checkm_data_2015_01_16.tar.gz && \
        mkdir -p /checkm_database \
		&& tar -xzf checkm_data_2015_01_16.tar.gz -C /checkm_database \
		&& rm -rf checkm_data_2015_01_16.tar.gz
RUN echo /checkm_database | checkm data setRoot /checkm_database

