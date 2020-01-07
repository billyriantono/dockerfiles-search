FROM nebtex/ubuntu-base:machine-learning

RUN apt-get -y update && \
    apt-get -y upgrade && \
    apt-get -y install npm nodejs nodejs-legacy wget locales git libpq-dev &&\
    locale-gen "en_US.UTF-8" && \
    apt-get remove -y locales && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV LANG en_US.UTF-8
ADD . /pip 
WORKDIR /pip

RUN pip3 install -r requirements.txt
RUN pip3 install git+https://github.com/NebTex/notebook

#Install Tensorflow
RUN wget  https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.10.0rc0-cp35-cp35m-linux_x86_64.whl
RUN pip3 install tensorflow-0.10.0rc0-cp35-cp35m-linux_x86_64.whl

# set tensorflow as bakend of keras
ENV KERAS_BACKEND=tensorflow

# install nodejs, utf8 locale
ENV DEBIAN_FRONTEND noninteractive
    
# install js dependencies
RUN npm install -g configurable-http-proxy && rm -rf ~/.npm

# install jupyterhub
RUN mkdir /src
RUN git clone https://github.com/jupyterhub/jupyterhub /src/jupyterhub
WORKDIR /src/jupyterhub

RUN python3 setup.py js && pip3 install . && \
    rm -rf $PWD ~/.cache ~/.npm

# install docker spawner
RUN git clone https://github.com/NebTex/dockerspawner.git /src/dockerspawner
WORKDIR /src/dockerspawner
RUN pip3 install -r requirements.txt && python3 setup.py install

# install github oauth for jupyterhub
RUN git clone https://github.com/jupyterhub/oauthenticator /src/oauthenticator
WORKDIR /src/oauthenticator
RUN pip3 install -r requirements.txt && python3 setup.py install

WORKDIR /
