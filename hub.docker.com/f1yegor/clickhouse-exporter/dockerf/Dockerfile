FROM eywalker/pydev:cuda

MAINTAINER Edgar Y. Walker <edgar.walker@gmail.com>

ADD requirements.txt /requirements.txt
RUN pip install -r /requirements.txt \
    && rm /requirements.txt \
    && mkdir /notebooks
ADD jupyter_notebook_config.py /root/.jupyter/jupyter_notebook_config.py
EXPOSE 8888
VOLUME /notebooks
WORKDIR /notebooks
CMD ["/bin/sh", "-c", "jupyter notebook"]

ADD start-singleuser.sh /usr/local/bin/
