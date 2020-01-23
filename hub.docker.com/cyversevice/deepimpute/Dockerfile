FROM cyversevice/jupyterlab-base:1.0.9
  
USER root

RUN apt-get update

RUN apt-get install -y git python3-pip

#RUN pip --no-cache-dir install tensorflow
RUN python3 -m ipykernel install --user
RUN git clone https://github.com/lanagarmire/deepimpute && cd deepimpute && pip install .

#WORKDIR /src/notebooks
#RUN chmod 777 /home/jovyan
RUN chmod 777 /home/jovyan/.local/share/jupyter
#RUN chmod 777 /src/notebooks
# Install and configure jupyter lab.
COPY jupyter_notebook_config.json /opt/conda/etc/jupyter/jupyter_notebook_config.json
# Change the user
USER jovyan
RUN usermod -d /home/jovyan -u 1000 jovyan
WORKDIR /home/jovyan
