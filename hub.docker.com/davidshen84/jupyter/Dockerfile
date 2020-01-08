FROM python:3
LABEL maintainer="Xi Shen <davidshen84@gmail.com>"

RUN pip3 install --upgrade pyzmq --install-option="--zmq=bundled" && \
    pip3 install --upgrade jupyter


VOLUME /notebook
WORKDIR /notebook

EXPOSE 8888

ENTRYPOINT jupyter notebook --ip=0.0.0.0 --allow-root --no-browser
