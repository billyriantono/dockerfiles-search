FROM jupyter/base-notebook

# Maintainer Sebastian Schmidt

USER root

RUN apt-get update && apt-get install -yq --no-install-recommends \
#    python3 \
#    python3-pip \
#    python3-setuptools \
    liblas-c3

# RUN pip install 'ggplot==0.6.8'

COPY requirements.txt /tmp/

RUN conda update -n base conda && \
    conda install psutil && \
    conda install -c plotly chart-studio
#    conda install -c blaze sqlite3

RUN pip install --requirement /tmp/requirements.txt && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
    
RUN mkdir data
COPY data/job461475_20156_73_87.las /home/jovyan/data/

RUN mkdir notebooks
COPY notebooks/plotly.ipynb /home/jovyan/notebooks/
