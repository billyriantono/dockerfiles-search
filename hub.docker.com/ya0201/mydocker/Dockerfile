# FROM nvidia/cuda:8.0-cudnn6-devel
# MAINTAINER me <me@abc.com>

# # working directory
# # mount application root directory on here (/app)
# RUN mkdir /app
# WORKDIR /app

# # set CUDA and cuDNN paths
# RUN echo -e "\n## CUDA and cuDNN paths"  >> ~/.bashrc && \
#     echo 'export PATH=/usr/local/cuda/bin:${PATH}' >> ~/.bashrc && \
#     echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH}' >> ~/.bashrc && \
#     echo 'export CUDA_PATH=/usr/local/cuda' >> ~/.bashrc

# # installation of git
# RUN apt-get update && apt-get -y install git

# # installation of python3.6
# RUN apt-get update && apt-get -y install software-properties-common && \
#     add-apt-repository ppa:jonathonf/python-3.6 && \
#     apt-get update && \
#     apt-get install -y python3.6

# # installation of pip3.6
# RUN apt-get update && apt-get -y install curl && \
#     curl https://bootstrap.pypa.io/get-pip.py | python3.6

# # installation of python3.6-dev
# RUN apt-get update && apt-get -y --no-install-recommends install python3.6-dev

# # installation of cupy and chainer
# RUN CUDA_PATH=/usr/local/cuda pip3.6 install cupy==4.0.0b3 chainer==4.0.0b3

# # installation of requirements
# RUN pip3.6 install numpy \
#                    librosa \
#                    pysptk \
#                    pyworld \
#                    fastdtw \
#                    nnmnkwii \
#                    matplotlib \
#                    chainerui

# # installation of world4py
# RUN git clone https://github.com/yamachu/WORLD4py.git && \
#     cd WORLD4py && \
#     python3.6 setup.py install && \
#     cd ../ && rm -rf WORLD4py

# # the default command that runs when docker container starts
# CMD echo "This is become-yukarin docker image..."


FROM chainer/chainer:latest-python3

# working directory
# mount application root directory on here (/app)
RUN mkdir /app
WORKDIR /app

# installation of git, vim
RUN apt-get update && apt-get -y install git vim

# installation of python3.6
RUN apt-get update && apt-get -y install software-properties-common && \
    add-apt-repository ppa:jonathonf/python-3.6 && \
    apt-get update && \
    apt-get install -y python3.6 && \
# installation of pip3.6
    apt-get update && apt-get -y install curl && \
    curl https://bootstrap.pypa.io/get-pip.py | python3.6 && \
# installation of python3.6-dev
    apt-get update && apt-get -y --no-install-recommends install python3.6-dev

# installation of ffmpeg
RUN apt-get update && apt-get -y install ffmpeg

# installation of requirements
# RUN pip3.6 install numpy
# RUN pip3.6 install librosa
# RUN pip3.6 install pysptk
# RUN pip3.6 install pyworld
# RUN pip3.6 install fastdtw
# RUN pip3.6 install nnmnkwii
# RUN pip3.6 install matplotlib
# RUN pip3.6 install chainerui
RUN pip3.6 install numpy
RUN pip3.6 install cupy
RUN pip3.6 install librosa
RUN pip3.6 install pysptk
RUN pip3.6 install pyworld
RUN pip3.6 install fastdtw
RUN pip3.6 install nnmnkwii
RUN pip3.6 install matplotlib
RUN pip3.6 install chainerui

# installation of world4py
RUN git clone https://github.com/yamachu/WORLD4py.git && \
    cd WORLD4py && \
    python3.6 setup.py install && \
    cd ../ && rm -rf WORLD4py

# the default command that runs when docker container starts
CMD echo "This is become-yukarin docker image..."
# CMD ["python", "train.py"]
