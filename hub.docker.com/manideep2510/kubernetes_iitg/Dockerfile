# Each instruction in this file generates a new layer that gets pushed to your local image cache
 
# Lines preceeded by # are regarded as comments and ignored
 
# The line below states we will base our new image on the Latest Official Ubuntu 
# Remove py3 for python 2 image
FROM tensorflow/tensorflow:1.13.1-gpu-py3
#ENV http_proxy http://172.16.117.121:3128
#ENV https_proxy http://172.16.117.121:3128

# Identify the maintainer of an image
LABEL maintainer="manideep2510@gmail.com"
LABEL version="0.1"
LABEL description="Tensorflow + some other libraries"

# Update the image to the latest packages
#RUN apt-get update && apt-get upgrade -y
RUN apt-get update


RUN apt-get install -y wget vim htop fish datamash graphviz libgraphviz-dev ffmpeg zsh tmux cmake

RUN apt-get install -y python3-venv

RUN pip3 --no-cache-dir install --upgrade pip

RUN pip3 --no-cache-dir install ipython pandas numpy jupyter cmake

RUN pip3 --no-cache-dir install docopt joblib natsort scipy 

RUN pip3 --no-cache-dir install tqdm matplotlib librosa scikit-learn ffmpeg

RUN pip3 --no-cache-dir install h5py imageio opencv-python Pillow 

RUN pip3 --no-cache-dir install scikit-image scikit-learn scikit-video scipy seaborn six sk-video

RUN pip3 --no-cache-dir install dlib funcsigs pydub

RUN pip3 --no-cache-dir install json5 Keras Keras-Applications Keras-Preprocessing

RUN pip3 --no-cache-dir install dill bleach namedtupled

RUN pip3 --no-cache-dir install PyEMD

RUN pip3 --no-cache-dir install torch torchvision transformers seqeval==0.0.5 nltk

RUN pip3 --no-cache-dir install networkx pathlib pygraphviz imgaug

RUN pip3 --no-cache-dir install Yarg==0.1.9 docopt==0.6.2

#RUN apt-get install -y python-all-dev python3-all-dev

RUN pip3 --no-cache-dir install nvgpu pipreqs asyncio mir_eval jiwer cython wandb

RUN pip3 --no-cache-dir install https://github.com/ludlows/python-pesq/archive/master.zip

RUN pip3 --no-cache-dir install pystoi

#asr-evaluation asrtoolkit SpeechRecognition

RUN curl -sL https://deb.nodesource.com/setup_13.x | bash

RUN apt-get install -y git nodejs

RUN pip3 --no-cache-dir install pymongo sacred

RUN npm install -g omniboard

#RUN apt-get install -y python-pyaudio python3-pyaudio

#RUN pip3 --no-cache-dir install google-cloud-speech

# RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

# Install locales
RUN apt-get install -y locales locales-all
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
