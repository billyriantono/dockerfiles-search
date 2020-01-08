FROM debian:stretch

ENV JUPYTER_CONFIG_DIR /root/.jupyter
ENV JUPYTER_NOTEBOOKS_DIR /opt/notebooks

RUN apt-get update && apt-get install -y apt-utils \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y python3 python3-pip \
 && ln -s /usr/bin/python3 /usr/bin/python \
 && ln -s /usr/bin/pip3 /usr/bin/pip \
 && pip install --no-cache-dir jupyter matplotlib \
 && mkdir $JUPYTER_NOTEBOOKS_DIR \
 && mkdir $JUPYTER_CONFIG_DIR \
 && rm -rf /var/lib/apt/lists/*

COPY jupyter_notebook_config.py $JUPYTER_CONFIG_DIR

EXPOSE 8888

CMD ["jupyter", "notebook"]
