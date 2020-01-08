ARG BASE_CONTAINER=jupyter/tensorflow-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Malaya Das <malaya.das@outlook.com>"

RUN conda config --set ssl_verify False
# Install Plotly


RUN pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org nbgitpuller && \
    jupyter serverextension enable --py nbgitpuller

RUN conda install --quiet --yes \
    'plotly=3.7*' \
    'pydot=1.3*' \
    'pandas=0.24*' \
    'pandas-datareader=0.7*' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

