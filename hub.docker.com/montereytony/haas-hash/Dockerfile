#
#    docker build --rm --tag haas-hash .
#
FROM jupyter/datascience-notebook
USER root
RUN ln -s /bin/tar /bin/gtar
RUN /usr/bin/apt-get install unzip
RUN /opt/conda/bin/pip install --upgrade pip
RUN /opt/conda/bin/pip install jupyterhub-hashauthenticator
RUN conda install -c conda-forge jupyter_contrib_nbextensions
RUN jupyter nbextension install --py widgetsnbextension --sys-prefix
RUN jupyter nbextension enable  --py widgetsnbextension --sys-prefix
USER jovyan
RUN jupyter nbextensions_configurator enable
