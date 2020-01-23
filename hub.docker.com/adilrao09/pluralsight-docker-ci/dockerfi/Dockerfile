ARG BASE_CONTAINER=eurodatacube/jupyterhub-edc
FROM $BASE_CONTAINER

USER $NB_UID

RUN git clone https://github.com/dcs4cop/xcube /tmp/xcube

RUN pip install nbgitpuller
RUN jupyter serverextension enable --py nbgitpuller --sys-prefix