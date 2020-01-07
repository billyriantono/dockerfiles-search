FROM frolvlad/alpine-miniconda3

RUN conda install -y -c pytorch faiss-cpu \
    && conda clean --all \
    && rm -rf /opt/conda/pkgs/*
