FROM python:3.6

ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT ["/usr/bin/tini", "--"]

ADD requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

ADD data/pull-data.sh /data/pull-data.sh
RUN /data/pull-data.sh

ADD docker/jupyter_notebook_config.py /root/.jupyter/jupyter_notebook_config.py

EXPOSE 8888
WORKDIR /notebook

CMD jupyter notebook --allow-root --ip 0.0.0.0

