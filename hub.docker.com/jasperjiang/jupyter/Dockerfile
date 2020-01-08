FROM ubuntu

RUN apt-get update
RUN apt-get install python3 python3-pip -y

RUN pip3 install jupyterlab

RUN jupyter notebook --generate-config

COPY jupyter_notebook_config.py ~/.jupyter/jupyter_notebook_config.py

ENTRYPOINT ["sh", "-c", "jupyter lab --port 8001 --no-browser --allow-root"]