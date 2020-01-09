FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04     
#9.1-cudnn7-devel-ubuntu16.04 #8.0-cudnn5-devel  #9.2-cudnn7-devel-ubuntu18.04

MAINTAINER Nobody

RUN apt-get update && \
    apt-get install -y curl build-essential libpng12-dev libffi-dev  && \
    apt-get clean && \
    rm -rf /var/tmp /tmp /var/lib/apt/lists/*

                              
RUN curl -sSL -o installer.sh https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh && \
    bash /installer.sh -b -f && \
    rm /installer.sh

ENV PATH "$PATH:/root/anaconda3/bin"

EXPOSE 8888 6006
VOLUME /notebooks
WORKDIR "/notebooks"

CMD jupyter notebook --no-browser --ip=0.0.0.0 --allow-root --NotebookApp.token= --NotebookApp.allow_origin='*'
# CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0"]

# docker run --rm -it -v $(pwd):/src tuananhktmt/keras-jupyter


# ADD https://github.com/tuananhvip/docker-keras-jupyter-gpu/raw/master/environment.yml /environment.yml
# RUN conda env update -f /environment.yml
