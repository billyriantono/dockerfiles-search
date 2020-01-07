FROM cmhi/cuda9.0-cudnn7

ENV TENSORFLOW_VERSION=1.7.0

RUN pip install --upgrade pip
# For how to run TensorFlow on Hadoop,
# please refer to https://www.tensorflow.org/deploy/hadoop
RUN pip install tensorflow-gpu==${TENSORFLOW_VERSION} && \
    pip3 install tensorflow-gpu==${TENSORFLOW_VERSION}

RUN pip3 install --upgrade tensorlayer==1.7.0

RUN pip install opencv-python && pip3 install opencv-python

# Add symbol link for libcuda.so
RUN ln -s /usr/local/cuda/targets/x86_64-linux/lib/stubs/libcuda.so \
          /usr/local/cuda/targets/x86_64-linux/lib/stubs/libcuda.so.1

#update and upgrade, install git
RUN apt-get update && apt-get upgrade -y && apt-get -y install git

ENV LC_ALL C

#if you want to build the docker image with data, please prepare the data first and remove the '#' in next line
#ADD ./data /tmp/data

WORKDIR /root
