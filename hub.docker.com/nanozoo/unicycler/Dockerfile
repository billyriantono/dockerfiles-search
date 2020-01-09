FROM continuumio/miniconda3
ENV VERSION 0.4.7-0

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda install -c bioconda unicycler=$VERSION && conda clean -a

# extend RAM usage in pilon to 12GB
RUN sed --in-place --follow-symlinks 's/Xmx1g/Xmx12g/' /opt/conda/bin/pilon
