FROM eliiza/spark-base:latest

WORKDIR /opt/spark/work-dir

# USER root
# RUN apk add --no-cache build-base libffi-dev openssl-dev python-dev && \
# USER jovyan
# RUN pip install cffi ipykernel ipython jupyter_client pycrypto

COPY common-python/requirements.txt /tmp/requirements.txt
RUN conda install --yes --file /tmp/requirements.txt

COPY kernel-launchers /usr/local/share/jupyter/kernel-launchers/

USER root
RUN chown -R jovyan:users /usr/local/share/jupyter /opt/spark/work-dir
USER jovyan
