FROM continuumio/miniconda3:latest

# update & upgrade
RUN apt-get -y update && \
    apt-get install --no-install-recommends -y build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# install python dependencies
RUN conda install -y python=3.6 \
 && conda install -y -c conda-forge -c pytorch -c fastai fastai=1.0.42 \
 && conda clean -y --all

