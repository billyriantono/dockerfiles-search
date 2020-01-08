FROM tensorflow/tensorflow:latest

RUN apt-get update && apt-get install -y git libhdf5-dev && rm -rf /var/lib/apt/*

RUN pip install --upgrade sklearn pandas scipy statsmodels seaborn xgboost h5py heraspy
RUN pip install --upgrade git+git://github.com/fchollet/keras.git --no-deps

ENV KERAS_BACKEND=tensorflow
