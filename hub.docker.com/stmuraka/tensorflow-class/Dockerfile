FROM ubuntu:xenial
MAINTAINER Shaun Murakami (stmuraka@gmail.com)

# instructions from https://docs.google.com/document/d/1jyRz6W6DzwHKWk2n7iwV8S_XFpeNu_6P-sbkixea1II/edit
RUN apt-get update \
 && apt-get install -y \
        build-essential \
        ca-certificates \
        vim \
        python3-dev \
        python3-setuptools \
 && apt-get autoremove \
 && apt-get autoclean \
 && ln -s /usr/bin/python3 /usr/bin/python \
 && easy_install3 pip \
 && pip install --upgrade pip \
 && pip install --upgrade virtualenv

# Create Virtualenv for tensorflow
#RUN virtualenv --system-site-packages -p python3 ~/tensorflow

# Activate the virtualenv environment
#RUN . ~/tensorflow/bin/activate

# Install TensorFlow
ARG TENSORFLOW_PKG="tensorflow"
#e.g. TENSORFLOW_PKG="https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.3.0-cp35-cp35m-linux_x86_64.whl"
RUN pip3 install --upgrade ${TENSORFLOW_PKG}

# Install Keras
RUN pip install keras

# Copy over test scripts
ADD test-tensorflow.py /root/
ADD test-keras.py /root/

# cd to homedir
WORKDIR /root/

# Expose 6006 for tensorboard graph
EXPOSE 6006
