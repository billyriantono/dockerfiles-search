FROM jupyter/scipy-notebook:latest

USER root

RUN apt-get update && apt-get install -y swig curl

RUN curl https://raw.githubusercontent.com/automl/auto-sklearn/master/requirements.txt | xargs -n 1 -L 1 pip install --default-timeout=100

RUN pip install --default-timeout=100 auto-sklearn

USER $NB_UID