FROM jupyter/base-notebook:latest
# https://hub.docker.com/r/jupyter/base-notebook/

MAINTAINER Adam Fekete "adam.fekete@kcl.ac.uk"
LABEL version="0.9"

RUN conda install --yes --quiet --no-update-dependencies \
    ase asap scikit-learn ipywidgets

RUN pip install --quiet --disable-pip-version-check nglview==1.0.b2 \
 && nglview install \
 && nglview enable \
 && jupyter nbextension enable nglview --py --sys-prefix


#ADD --chown=jovyan:users notebooks /home/jovyan/
ADD notebooks /home/jovyan/

# Final permissions fix
USER root
RUN sudo chown --recursive jovyan:users .
USER jovyan
