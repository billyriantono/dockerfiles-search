# use Ubuntu LTS
FROM ubuntu:16.04

RUN apt-get update
RUN apt-get upgrade --yes
RUN apt-get install --no-install-recommends --yes \
    apt-utils \
    gcc \
    nano \
    vim \
    unzip \
    bzip2 \
    curl \
    wget \
    graphviz

# Anaconda installing
RUN wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    --no-check-certificate --quiet
RUN bash Miniconda3-latest-Linux-x86_64.sh -b
RUN rm Miniconda3-latest-Linux-x86_64.sh
# Set path to conda
ENV PATH /root/miniconda3/bin:$PATH
# Updating Anaconda packages
RUN conda config --add channels conda-forge 
RUN conda update conda --yes

# install required packages
COPY requirements.txt /
RUN conda install --yes --file requirements.txt


# Jupyter configs
RUN jupyter notebook --allow-root --generate-config -y
# Passwordless login
RUN echo "c.NotebookApp.password = ''" >> ~/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.token = ''" >> ~/.jupyter/jupyter_notebook_config.py

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents
# kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]


# setup jlab
RUN jupyter serverextension enable --py jupyterlab

# setup jlab-bokeh extention
#RUN jupyter labextension install jupyterlab_bokeh

# Jupyter listens port: 8888
EXPOSE 8888
# Run Jupyter notebook as Docker main process

# Always run jlab when docker image is spun-up
CMD [  "jupyter" \
     , "lab" \
     , "--allow-root" \
     , "--ip=0.0.0.0" \
     , "--port=8888" \
     , "--no-browser" \
     , "--notebook-dir=./"]
