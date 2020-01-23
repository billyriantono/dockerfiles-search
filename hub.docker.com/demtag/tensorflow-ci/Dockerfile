FROM tensorflow/tensorflow:1.12.0-py3

RUN curl --silent --location https://deb.nodesource.com/setup_10.x | bash -

RUN apt-get install --yes nodejs git \
    && npm install -g @tensorflow/tfjs @tensorflow/tfjs-node \
    && pip3 install tensorflowjs
