FROM continuumio/anaconda3:5.2.0
WORKDIR /workspace
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y python-numpy python-dev cmake zlib1g-dev libjpeg-dev xvfb ffmpeg xorg-dev python-opengl libboost-all-dev libsdl2-dev swig && \
    apt-get clean  && \
    rm -rf /var/lib/apt/lists/* && \
    conda update -n base conda && \
    conda install -y numpy pandas scipy scikit-learn matplotlib tensorflow tqdm pillow cython seaborn && \
    conda update numpy pandas scipy scikit-learn matplotlib tensorflow tqdm pillow cython seaborn && \
    conda install -y pytorch=1.3.1 torchvision -c pytorch// && \
    pip install --no-cache-dir gym 'gym[all]' && \
    pip install --no-cache-dir pygame==1.9.4 && \
    pip install --no-cache-dir -e git+https://github.com/ntasfi/PyGame-Learning-Environment.git#egg=ple && \
    pip install --no-cache-dir -e git+https://github.com/lusob/gym-ple.git#egg=gym-ple && \
    pip install --no-cache-dir flask smart_getenv gunicorn && \
    conda install -y -c caffe2 caffe2 protobuf && \
    conda install -y -c conda-forge onnx
CMD jupyter-lab --port=8888 --ip=0.0.0.0 --allow-root