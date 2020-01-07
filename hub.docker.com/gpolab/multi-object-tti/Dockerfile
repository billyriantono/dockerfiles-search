FROM pytorch/pytorch:0.4.1-cuda9-cudnn7-devel

RUN apt-get update && apt-get install -y git htop less graphviz && apt-get clean
RUN conda install -y numpy
RUN pip install --upgrade pip && pip install Cython && \
    pip install --upgrade torch==1.0.0 && pip install pycocotools matplotlib\
    pytest spacy pytorch-nlp dill torchviz torchvision

RUN python -m spacy download en
ENV PYTHONPATH /opt/project
WORKDIR /workspace
