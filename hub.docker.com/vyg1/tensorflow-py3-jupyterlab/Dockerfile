FROM tensorflow/tensorflow:latest-py3
LABEL maintainer="vyg178@163.com"

RUN \
    pip install jupyterlab \
    && pip install keras

CMD ["jupyter", "lab", "--allow-root"]