# This Dockerfile defines an image that contains all the dependencies that are needed to run MBRL.
# Note that it doesn't contain MBRL itself.

FROM continuumio/miniconda3

RUN conda install pytorch torchvision cudatoolkit=10.0 -c pytorch
RUN pip install tensorboardx

#Install MuJoCo
#Install OpenAI's gym

