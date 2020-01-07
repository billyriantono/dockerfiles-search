########## Dockerfile He+ tensorflow-pytorch 1.0 ############

FROM jupyter/tensorflow-notebook:7f1482f5a136

###RUN mkdir -p /home/$NB_UID

ENV NB_USER=$NB_USER \
    NB_UID=$NB_UID

WORKDIR /home/$NB_USER

USER $NB_USER

COPY requirements.txt /tmp/

RUN conda install --yes --file /tmp/requirements.txt && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

##COPY ./Autoencoder_DL/ /home/$NB_UID/Autoencoder_DL/ \
##     chmod +x /home/$NB_UID/Autoencoder_DL

EXPOSE 8888
