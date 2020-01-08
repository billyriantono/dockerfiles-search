FROM continuumio/miniconda3
ENV VERSION 1.0 

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda config --add channels conda-forge && \
    conda config --add channels bioconda && \
    conda config --add channels default

RUN conda install biopython pandas tqdm matplotlib scipy scikit-learn hdbscan umap-learn mummer && conda clean -a

RUN git clone https://github.com/hoelzer/marine-phage-paper-scripts.git
ENV PATH /marine-phage-paper-scripts:$PATH

RUN for SCRIPT in /marine-phage-paper-scripts/*.py; do sed -i '1s/^/#!\/usr\/bin\/env python \n\n/' $SCRIPT; chmod +x $SCRIPT; done
