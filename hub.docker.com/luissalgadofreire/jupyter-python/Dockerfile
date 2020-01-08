# Dockerfile based on jupyter/minimal-notebook.
# See: https://github.com/jupyter/docker-stacks/tree/master/minimal-notebook

FROM jupyter/minimal-notebook

MAINTAINER Luis Freire

USER root

# Install all OS dependencies for openai gym
RUN apt-get update && apt-get install -yq --no-install-recommends \
    python-numpy \
    python-dev \
    cmake \
    zlib1g-dev \
    libjpeg-dev \
    xvfb \
    libav-tools \
    xorg-dev \
    python-opengl \
    libboost-all-dev \
    libsdl2-dev \
    swig \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install ffmpeg for video handling
RUN echo "deb http://ftp.uk.debian.org/debian jessie-backports main" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -yq --no-install-recommends ffmpeg

# Add channels to conda to install custom packages
RUN conda config --add channels menpo       # for opencv

# Set the working directory
WORKDIR /home/$NB_USER/work

# Install binary packages with conda
# Remove pyqt and qt pulled in for matplotlib since we're only ever going to
# use notebook-friendly backends in these images
RUN conda install --quiet --yes \
    'nomkl' \
    'ipywidgets=6.0*' \
    'pandas=0.19*' \
    'numexpr=2.6*' \
    'matplotlib=2.0*' \
    'scipy=0.19*' \
    'seaborn=0.7*' \
    'scikit-learn=0.18*' \
    'scikit-image=0.12*' \
    'sympy=1.0*' \
    'cython=0.25*' \
    'patsy=0.4*' \
    'statsmodels=0.8*' \
    'cloudpickle=0.2*' \
    'dill=0.2*' \
    'numba=0.31*' \
    'bokeh=0.12*' \
    'sqlalchemy=1.1*' \
    'hdf5=1.8.17' \
    'h5py=2.6*' \
    'vincent=0.4.*' \
    'beautifulsoup4=4.5.*' \
    'xlrd' \
    'networkx' \
    'nltk' \
    'opencv3' \
    'graphviz' \
    'theano' && \
    conda remove --quiet --yes --force qt pyqt && \
    conda clean -tipsy

# Install python packages with pip
RUN pip install --no-cache-dir \
    'Pillow==3.3.1' \
    'Babel==2.3.4' \
    'sphinx==1.4.6' \
    'sphinx_rtd_theme' \
    'python-slugify' \
    'pyprind' \
    'keras' \
    'autograd' \
    'gym[atari]'

# Activate ipywidgets extension in the environment that runs the notebook server
RUN jupyter nbextension enable --py widgetsnbextension --sys-prefix

# Switch back to jovyan to avoid accidental container runs as root
USER $NB_USER
