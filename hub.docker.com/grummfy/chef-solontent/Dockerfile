FROM jupyter/datascience-notebook:latest

USER root
RUN apt update && \
    apt install build-essential libpq-dev && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

RUN pip install xgboost featuretools graphviz \
    jupyter_nbextensions_configurator \
    pyyaml ua-parser user-agents fuzzywuzzy[speedup] tabulate \
    imblearn \
    holidays \
    psycopg2 && \
    jupyter nbextensions_configurator enable --user && \
    conda install bokeh -c bokeh
