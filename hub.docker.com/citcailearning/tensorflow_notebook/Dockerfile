#ubuntu16.04
#karas = 2.0.2
#tensorflow = 1.0.1
#gpu cuda8.0

FROM citcailearning/scipy_gpu_runtime_notebook:cuda8.0

MAINTAINER Mad Chang <citcailearning@gmail.com>

RUN /opt/conda/bin/pip install tensorflow==1.0.1
RUN /opt/conda/bin/pip install keras==2.0.2

USER $NB_USER
