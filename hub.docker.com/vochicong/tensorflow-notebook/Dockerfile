FROM jupyter/tensorflow-notebook

USER root
RUN apt-get update &&\
    apt-get install -y fonts-ipafont-gothic &&\
    apt-get clean
USER $NB_USER
RUN rm ~/.cache/matplotlib/fontList.json
