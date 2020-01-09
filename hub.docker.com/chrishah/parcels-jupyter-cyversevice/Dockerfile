FROM cyversevice/jupyterlab-base:1.0.9

USER root

RUN apt-get update && apt-get -y upgrade && apt-get install -y --allow-downgrades gcc=4:7.3.0-3ubuntu2 && \
#RUN apt-get update && apt-get -y upgrade && apt-get install -y && \
        apt-get clean && apt-get purge && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda install conda=4.6.8
RUN conda install --yes netcdf4=1.4.1 cartopy=0.17.0 ffmpeg=4.1.1 parcels
#RUN parcels_get_examples parcels_examples

USER $NB_USER

