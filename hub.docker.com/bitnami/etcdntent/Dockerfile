FROM continuumio/miniconda3

#  $ docker build . -t bitbeamer/jupyter:latest -t bitbeamer/jupyter:1.0.0
#  $ docker run -d -p 443:8888 -v /mnt/volume_fra1_01/notebook/:/notebook -v /mnt/volume_fra1_01/config/:/config bitbeamer/jupyter:latest
#  $ docker exec -it clever_ramanujan bash
#  $ docker run --rm -it bitbeamer/jupyter:latest /bin/bash
#  $ docker push bitbeamer/jupyter:latest
#  $ docker push bitbeamer/jupyter:1.0.0

# Install required packages
RUN apt update && apt-get upgrade -y --force-yes -qq && apt install gcc -y
RUN conda install jupyter pandas numpy matplotlib xlrd plotly elasticsearch jupyterlab nodejs ipywidgets -y
RUN jupyter nbextension enable --py widgetsnbextension
RUN pip install jupyterlab-git && jupyter serverextension enable --py jupyterlab_git
RUN mkdir /notebook && mkdir /config

#RUN jupyter labextension install jupyterlab-drawio
ENV LANG=C.UTF-8

# Expose Jupyter port & cmd
EXPOSE 8888

CMD jupyter lab --config /config/jupyter/jupyter_notebook_config.py