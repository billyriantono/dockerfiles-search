FROM jupyter/datascience-notebook:latest

USER root

RUN apt-get update && apt-get install -y proj-bin libproj-dev libgeos-dev openssh-server libspatialindex-dev libpq-dev htop

USER $NB_UID

COPY requirements.txt /tmp/

RUN mkdir -p code/jupyter_detektor && chown -R jovyan:users /home/jovyan/code/ && chown -R jovyan:users /home/jovyan/code/jupyter_detektor/

WORKDIR code/jupyter_detektor

COPY --chown=jovyan:users . .

RUN pip install --requirement /tmp/requirements.txt && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

WORKDIR ../

RUN git clone https://github.com/LeandroOrdonez/gpd_lite_toolbox.git

WORKDIR gpd_lite_toolbox/

RUN python setup.py install

WORKDIR ../jupyter_detektor

USER $NB_UID