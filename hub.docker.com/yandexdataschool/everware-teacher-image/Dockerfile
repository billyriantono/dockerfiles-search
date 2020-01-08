FROM jupyterhub/singleuser@sha256:5dd681bb378274d57c89116e9e1d4741716f72b90a6bda7d8397d1e1d6d89ef2

USER root

RUN apt-get update
RUN apt-get install -y libgl1-mesa-glx git gcc

ADD requirements.txt requirements.txt
RUN pip install -r requirements.txt

RUN jupyter contrib nbextension install --sys-prefix

RUN jupyter nbextension install --sys-prefix --py nbgrader --overwrite
RUN jupyter nbextension enable --sys-prefix --py nbgrader
RUN jupyter nbextension enable --sys-prefix toc2/main

RUN jupyter serverextension enable --sys-prefix --py nbgrader
RUN jupyter nbextensions_configurator disable --sys-prefix

RUN mkdir -p /exchange && chmod -R 777 /exchange
VOLUME ["/exchange"]

USER jovyan