FROM eliiza/dsp-base:latest

LABEL maintainer="Ray Hilton <ray.hilton@eliiza.com.au>"

RUN conda uninstall jupyterlab && \
    pip install s3contents

COPY config/jupyter_notebook_config.py jupyter_notebook_config.py
RUN cat jupyter_notebook_config.py >>/etc/jupyter/jupyter_notebook_config.py && \
    rm -f jupyter_notebook_config.py
