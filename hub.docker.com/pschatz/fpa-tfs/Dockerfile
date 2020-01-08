
FROM ubuntu:16.04

MAINTAINER Jeremiah Harmsen <jeremiah@google.com>

RUN apt-get update && apt-get install -y \
        build-essential \
        curl \
        git \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        mlocate \
        pkg-config \
        python-dev \
        python-numpy \
        python-pip \
        software-properties-common \
        swig \
        zip \
        zlib1g-dev \
        libcurl3-dev \
        openjdk-8-jdk\
        openjdk-8-jre-headless \
        wget \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set up grpc

RUN pip install mock grpcio


#
# We (Pete and opensource community) got errors on serving code after a build in early march
# article (https://github.com/tensorflow/serving/issues/819)said to run the following commands.
# Pete ran manually and it resolved, so we are going to add those commands here
# Had to add the --yes to skip confirmation questions
#
RUN add-apt-repository --yes ppa:ubuntu-toolchain-r/test
RUN apt-get --yes update
RUN apt-get --yes upgrade
RUN apt-get --yes dist-upgrade

# install TensorFlow Serving Python API PIP package (taken from https://www.tensorflow.org/serving/setup#prerequisites)
RUN pip install tensorflow-serving-api


#
# remove any old binaries then install the TensorFlow Serving ModelServer binary (taken from https://www.tensorflow.org/serving/setup#prerequisites)
#
# Note: Make sure to remove sudo from any commands that are pasted from the web site
#
# remove the old binaries
#RUN apt-get remove tensorflow-model-server

# Add TensorFlow Serving distribution URI as a package source (one time setup)
RUN echo "deb [arch=amd64] http://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server tensorflow-model-server-universal" | tee /etc/apt/sources.list.d/tensorflow-serving.list
RUN curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | apt-key add -

# Install and update TensorFlow ModelServer
RUN apt-get update && apt-get install tensorflow-model-server




# Set up Bazel.

ENV BAZELRC /root/.bazelrc
# Install the most recent bazel release.
ENV BAZEL_VERSION 0.5.4
WORKDIR /
RUN mkdir /bazel && \
    cd /bazel && \
    curl -fSsL -O https://github.com/bazelbuild/bazel/releases/download/$BAZEL_VERSION/bazel-$BAZEL_VERSION-installer-linux-x86_64.sh && \
    curl -fSsL -o /bazel/LICENSE.txt https://raw.githubusercontent.com/bazelbuild/bazel/master/LICENSE && \
    chmod +x bazel-*.sh && \
    ./bazel-$BAZEL_VERSION-installer-linux-x86_64.sh && \
    cd / && \
    rm -f /bazel/bazel-$BAZEL_VERSION-installer-linux-x86_64.sh


#
# Copy In Python code
#
RUN mkdir -p /tensorflow_serving/example
COPY ./mnist_saved_model.py /tensorflow_serving/example/mnist_saved_model.py
COPY ./mnist_input_data.py /tensorflow_serving/example/mnist_input_data.py
COPY ./mnist_client.py /tensorflow_serving/example/mnist_client.py
COPY ./ServerStartupScript /ServerStartupScript

## Train the model
#RUN python tensorflow_serving/example/mnist_saved_model.py /tmp/mnist_model
#
## Load the server with the model
#RUN tensorflow_model_server --port=9000 --model_name=mnist --model_base_path=/tmp/mnist_model/ &

# tell the port number the container should expose
EXPOSE 9000

# run a startup script in a command shell 
CMD ["/bin/bash", "/ServerStartupScript"]
