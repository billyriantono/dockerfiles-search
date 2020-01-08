FROM jupyter/pyspark-notebook:a95cb64dfe10

USER root

RUN apt-get update

# iRODS iCommands
RUN wget https://s3-us-west-1.amazonaws.com/atmosphere-ansible-files/irods-icommands-4.1.9-cv-64bit-ubuntu-14.deb
RUN dpkg -i irods-icommands-4.1.9-cv-64bit-ubuntu-14.deb
RUN rm irods-icommands-4.1.9-cv-64bit-ubuntu-14.deb

# Get npm required for Jupyter Lab extensions
# https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04
RUN apt-get -y install npm

# RUN apt-get -y install python3-pip
RUN conda install pip
RUN pip install \
    jupyterlab \
    jupyterlab_irods
# From https://github.com/towicode/IJab
RUN jupyter serverextension enable --py jupyterlab_irods
RUN jupyter labextension install @jupyterlab/hub-extension
RUN jupyter labextension install ijab

USER jovyan


CMD ["jupyterhub-singleuser"]
