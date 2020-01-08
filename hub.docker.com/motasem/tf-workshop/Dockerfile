FROM tensorflow/tensorflow:latest-py3

MAINTAINER motasem@gmail.com


RUN pip install --no-cache-dir --upgrade pip && \
    pip --no-cache-dir install \
    statsmodels \
    seaborn \
    keras \
    Cython \
    gensim 


COPY workshop /notebooks/workshop
EXPOSE 8888 6006

