FROM cyversevice/jupyterlab-base:1.0.9
USER root
RUN apt-get update && \
    apt-get install -y libbz2-dev libssl-dev libcurl4-openssl-dev zlib1g-dev
RUN pip install kipoi kipoiseq torch

# install jupyterlab git extension
RUN jupyter labextension install @jupyterlab/git && \
        pip install --upgrade jupyterlab-git && \
        jupyter serverextension enable --py jupyterlab_git

# install jupyterlab github extension
RUN jupyter labextension install @jupyterlab/github

# install jupyterlab gitlab extension
RUN jupyter labextension install jupyterlab-gitlab

# Change the user
USER jovyan
