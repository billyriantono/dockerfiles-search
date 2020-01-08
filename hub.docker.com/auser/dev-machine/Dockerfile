FROM uetchy/machinelearning

MAINTAINER Ari Lerner

USER root

# Install Python packages
# RUN conda create --quiet --yes -n py3 python=3.4 && \
#     conda create --quiet --yes -n py2 python=2.7


# Base
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

WORKDIR /usr/local/src
RUN apt-get install -yq \
        libzmq3-dev libssl-dev python-zmq luajit luarocks \
        libqt4-gui \
        git-core gnuplot-x11 ipython libwxbase2.8-0 libwxgtk2.8-0 \
        python-decorator \
        python-pexpect python-simplegeneric
# Torch7 installation scripts - http://torch.ch/docs/getting-started.html
RUN git clone https://github.com/torch/distro.git torch --recursive

RUN cd /usr/local/src/torch && bash install-deps
RUN cd /usr/local/src/torch && ./install.sh

ENV PATH=/usr/local/src/torch/install/bin:$PATH

WORKDIR /usr/local/src/
RUN luarocks install lzmq && \
    git clone https://github.com/facebook/iTorch.git

RUN cd /usr/local/src/iTorch && \
    luarocks make 


# RUN conda install --yes -c https://conda.anaconda.org/anaconda setuptools && \
#  source activate py2 && \
#     pip install --ignore-installed --upgrade keras tensorflow scipy && \
#  source activate py3 && \
#     pip install --ignore-installed --upgrade keras tensorflow scipy

COPY ./requirements.txt /tmp/requirements.txt

# RUN source activate py2 && \
#     conda install notebook ipykernel && \
#     ipython kernel install --user && \
RUN conda install --yes -c https://conda.anaconda.org/anaconda setuptools && \
    conda install -y -c https://conda.anaconda.org/menpo menpo menpoprojects opencv3 && \
    conda install -y -c conda-forge tensorflow flask-socketio eventlet && \
    pip install --upgrade -r /tmp/requirements.txt && \
    rm /tmp/requirements.txt


# RUN source activate py3 && \
#     conda install notebook ipykernel && \
#     ipython kernel install --user && \
#     pip install -r /tmp/requirements.txt

# RUN conda install -n py2 -y scikit-learn && \
#     conda install -n py2 -y -c https://conda.anaconda.org/menpo opencv3 && \
#     conda install -n py2 -y -c conda-forge tensorflow flask-socketio eventlet

# RUN conda install -n py3 -y scikit-learn && \
#     conda install -n py3 -y -c https://conda.anaconda.org/menpo opencv3 && \
#     conda install -n py3 -y -c conda-forge tensorflow flask-socketio eventlet

# RUN echo "jt -T -cellw 1400 -t chesterish -fs 8 -nfs 6 -tfs 6" > /bin/jupyter_theme.sh && chmod a+x /bin/jupyter_theme.sh

# RUN mkdir ~/.keras && echo "{ \"image_dim_ordering\": \"tf\", \"epsilon\": 1e-07, \"backend\": \"tensorflow\", \"floatx\": \"float32\" }" >  ~/.keras/keras.json

# RUN which python2 && which python3
# RUN (echo "import imageio"; echo "imageio.plugins.ffmpeg.download()") | python2
# RUN (echo "import imageio"; echo "imageio.plugins.ffmpeg.download()") | python3
