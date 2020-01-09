######### Dockerfile He+ Autoencoder Advanced with read-write ###########
FROM jupyter/tensorflow-notebook:7f1482f5a136
###RUN mkdir -p /home/$NB_UID
ENV NB_USER=$NB_USER \
    NB_UID=$NB_UID
WORKDIR /home/$NB_USER
COPY Autoencoder_DL /home/$NB_UID/Autoencoder_DL
COPY requirements.txt /tmp/
USER root
RUN chmod +x /home/$NB_UID/Autoencoder_DL/
USER $NB_USER
RUN conda install --yes --file /tmp/requirements.txt && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
WORKDIR /home/$NB_UID
EXPOSE 8888

