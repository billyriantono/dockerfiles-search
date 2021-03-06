# fork from https://github.com/facebookresearch/Detectron/blob/master/docker/Dockerfile

# Use Caffe2 image as parent image
FROM caffe2/caffe2:snapshot-py2-cuda9.0-cudnn7-ubuntu16.04

RUN mv /usr/local/caffe2 /usr/local/caffe2_build
ENV Caffe2_DIR /usr/local/caffe2_build
ENV PYTHONPATH /usr/local/caffe2_build:${PYTHONPATH}
ENV LD_LIBRARY_PATH /usr/local/caffe2_build/lib:${LD_LIBRARY_PATH}
ENV Software_DIR /download

# Install Detectron &  COCO API
RUN mkdir ${Software_DIR} && \
        git clone https://github.com/facebookresearch/detectron ${Software_DIR}/detectron && \
        pip install -r ${Software_DIR}/detectron/requirements.txt && \
        git clone https://github.com/cocodataset/cocoapi.git ${Software_DIR}/cocoapi && \
        cd ${Software_DIR}/cocoapi/PythonAPI  && \
        make install && \
        cd ${Software_DIR}/detectron && make && make ops


###### Add by xusong ######

# Install Densepose: https://github.com/facebookresearch/DensePose/blob/master/INSTALL.md#densepose
#                    https://github.com/facebookresearch/DensePose/blob/master/docker/Dockerfile
RUN git clone https://github.com/facebookresearch/densepose ${Software_DIR}/densepose && \
        cd ${Software_DIR}/densepose && \
        pip install -r requirements.txt && \
        make && make ops

# Install others
RUN pip install pydot jupyterlab

RUN apt-get update && \
        apt-get install -y wget vim

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

WORKDIR "/root/"


CMD ["jupyter", "lab", "--ip=127.0.0.1", "--allow-root"]
