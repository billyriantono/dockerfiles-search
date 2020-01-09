FROM ubuntu:18.04
RUN apt-get update && apt-get -y install python python-dev python-pip wget
RUN pip install apache-beam
RUN wget https://raw.githubusercontent.com/google/deepvariant/r0.9/tools/shuffle_tfrecords_beam.py
