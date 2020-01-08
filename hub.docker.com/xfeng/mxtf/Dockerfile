FROM dsdgroup/mxnet:gpu-cuda-8.0
MAINTAINER XiaoFeng Qi <seal.qi@foxmail.com>

# install opencv
RUN apt-get update && apt-get install -y python-opencv && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# get rid of "libdc1394 error: Failed to initialize libdc1394"
RUN ln /dev/null /dev/raw1394

# install python packages
RUN pip install --upgrade \
    numpy \
    Flask \
    Flask-Babel \
    Flask-Login \
    Flask-Mail \
    Flask-OpenID \
    Flask-SocketIO \
    Flask-SQLAlchemy \
    Flask-WhooshAlchemy \
    Flask-WTF \
    gensim \
    gevent \
    gevent-websocket \
    jieba \
    scikit-image \
    scikit-learn

# install tensorflow
RUN pip --no-cache-dir install \
    https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-0.12.0rc0-cp27-none-linux_x86_64.whl

# expose the default ports of jupyter,flask and tomcat
EXPOSE 8888
EXPOSE 5000
EXPOSE 8080

# Set a seperated workspace as working directory
WORKDIR /root/workspace
# Optionally expose the workspace to the host
VOLUME ["/root/workspace"]