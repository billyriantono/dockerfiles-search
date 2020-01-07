FROM python:3.6-slim

RUN pip3 install tensorflow==1.4
RUN pip3 install http://download.pytorch.org/whl/cpu/torch-0.4.0-cp36-cp36m-linux_x86_64.whl
RUN pip3 install torchvision
RUN pip3 install keras
RUN pip3 install opencv-python
RUN pip3 install easydict
RUN pip3 install Cython
RUN pip3 install grpcio-tools
RUN pip3 install googleapis-common-protos

RUN apt-get update && apt-get -y install gcc \
    && apt-get -y install libglib2.0-0 \
    && apt-get -y install libsm6 \
    && apt-get -y install libfontconfig1 libxrender1 \
    && apt-get -y install libxext6

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# run python for test

ENTRYPOINT ["/usr/local/bin/python"]
