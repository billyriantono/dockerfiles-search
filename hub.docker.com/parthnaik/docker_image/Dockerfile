# Base image
FROM python:3.6.3

# Updating repository sources
RUN apt-get update

# Install tensorflow
RUN pip install --upgrade \
  https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.4.0-cp36-cp36m-linux_x86_64.whl

#Updating pip to fix scipy installation error
RUN python3 -m pip install --upgrade pip

# Copying requirements.txt file
COPY requirements.txt requirements.txt

# pip install 
RUN pip install --no-cache -r requirements.txt
