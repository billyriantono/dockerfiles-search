FROM jupyter/scipy-notebook
RUN conda install -c pytorch pytorch-cpu torchvision-cpu
RUN conda install -c anaconda tensorflow
RUN conda install -c conda-forge geoalchemy2 
RUN conda install shapely keras cartopy psycopg2
RUN conda install -c conda-forge simplekml 
ENV JUPYTER_ENABLE_LAB=yes
ENV GRANT_SUDO=yes
ENV GEN_CERT=yes
USER root
RUN apt update && apt install -y gdal-bin
