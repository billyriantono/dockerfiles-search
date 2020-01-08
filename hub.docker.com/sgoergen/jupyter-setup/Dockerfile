#!/usr/bin/bash
FROM continuumio/miniconda3 

# ENVIRONMENT
ENV TERM=xterm
ENV SHELL=/bin/bash
ENV LANG en_US.UTF-8

# TINI
# Operates as process subreaper for jupyter and prevents kernel crashes  
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

# APT-GET
ADD apt-packages.txt /tmp/apt-packages.txt
RUN apt-get update  -y 
RUN apt-get install -y apt-utils build-essential 
RUN xargs -a /tmp/apt-packages.txt apt-get install -y

# CONDA
ADD /requirements/ /tmp/requirements
RUN conda install --yes --file /tmp/requirements/conda.txt
RUN conda install --yes --file /tmp/requirements/conda-forge.txt -c conda-forge

# JUPYTER
RUN mkdir -p /home/ds/notebooks
ENV HOME=/home/ds
VOLUME /home/ds/notebooks
WORKDIR /home/ds/notebooks

EXPOSE 8888

# Password = "haskell"
CMD [ "jupyter" \
    , "notebook" \
    , "--allow-root" \
    , "--port=8888" \
    , "--no-browser" \
    , "--NotebookApp.password='sha1:996e62635574:9a1e923102f23554ebead459812c2245827c5f75'" \
    , "--ip=0.0.0.0"]

