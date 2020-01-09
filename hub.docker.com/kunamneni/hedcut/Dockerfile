FROM continuumio/anaconda3

RUN conda update -y -n base -c defaults conda
RUN conda install -y -c conda-forge opencv && \
    conda install -y -c anaconda progressbar2 && \
    conda install -y -c conda-forge tensorflow && \
    conda install -y -c conda-forge keras && \
    conda install -y -c pytorch pytorch && \
    conda install -y -c pytorch torchvision && \
    conda install -y -c conda-forge dominate && \
    conda install -y -c conda-forge visdom

CMD bash
