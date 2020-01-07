FROM ftieben/miniconda:alpine as conda-base

LABEL MAINTAINER Florian Tieben <ftiebe@gmail.com>

RUN conda install -c conda-forge tensorflow pandas &&\
conda clean --all

CMD ["python3"]