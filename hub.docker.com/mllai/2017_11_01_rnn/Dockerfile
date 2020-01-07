FROM tensorflow/tensorflow:1.3.0-py3 

LABEL maintainer="Nick Ma <www.github.com/nma>"

RUN mkdir /notebooks/2017_11_01_RNN

COPY . /notebooks/2017_11_01_RNN

# Fix plots not showing up with default tensorflow image
RUN pip --no-cache-dir install matplotlib==2.1.0 jupyter-client==5.1.0 jupyter-console==5.2.0 jupyter-core==4.3.0

