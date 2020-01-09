# use base python image with python 3
#FROM python:3.6
FROM tensorflow/tensorflow:latest-gpu-py3

ENV PYTHONUNBUFFERED 1

# install python dependencies
#RUN apt-get update && \
#    apt-get upgrade -y && \
#    apt-get install git -y && \
RUN pip install --upgrade pip && \
    pip install tensorflow-gpu==1.12.0 nltk==3.3 numpy==1.15.2 colorama==0.3.9 tqdm==4.28.1 sacremoses stanfordcorenlp && \
    python3 -m nltk.downloader -d /usr/share/nltk_data stopwords perluniprops punkt

# create unprivileged user
RUN adduser --disabled-password --gecos '' myuser



# FROM tensorflow/tensorflow:1.4.1
# RUN pip install colorama==0.3.9
# RUN pip install nltk==3.2.5
# RUN pip install numpy==1.14.0
# RUN pip install six==1.11.0
# RUN pip install tensorflow-tensorboard==0.4.0
# RUN pip install tqdm==4.19.5
# RUN python3 -m nltk.downloader --dir=/usr/local/share/nltk_data perluniprops punkt
