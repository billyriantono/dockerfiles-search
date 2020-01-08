# Build from a recent python3 version (64 bit python required for Tensorflow)
FROM ubuntu:16.04
FROM python:3.6.5-onbuild
COPY requirements.txt requirements.txt

# Install required python modules
RUN pip3 install -r requirements.txt

# An RGB input image for local debug/testing
# Move it to the root dir where inference code (and tutorial) expects to find it
RUN mv 2568.tif /2568.tif

# Rename the trained checkpoint from the baseline model release to `model.pb`
# so that the `run.sh` file will find and use it
RUN mv multiresfinetuned5296.pb model.pb

#give permission to run shell script
RUN chmod 177 run.sh 
