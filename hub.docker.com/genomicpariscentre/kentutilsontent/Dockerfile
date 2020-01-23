ARG BASE_CONTAINER=jupyter/scipy-notebook
FROM $BASE_CONTAINER

ARG CLASS_GIT_REPO=https://github.com/data-8/materials-fa18
ARG CLASS_FOLDER_NAME=data-8
    
USER $NB_UID

RUN git clone $CLASS_GIT_REPO /home/$NB_USER/$CLASS_FOLDER_NAME/ && \
    rm -rf /home/$NB_USER/.local && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
