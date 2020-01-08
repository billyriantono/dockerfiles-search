# Copyright (c) Niels Borie.

FROM jupyter/tensorflow-notebook:5811dcb711ba

LABEL maintainer="SKW"

USER root

# --- Install python-tk htop python-boost
RUN apt-get update && \
    apt-get install -y --no-install-recommends python-tk software-properties-common htop libboost-all-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# --- Install dependency gcc/g++
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test

# --- Install gcc/g++
RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc-7 g++-7 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# --- Update alternatives
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 60 --slave /usr/bin/g++ g++ /usr/bin/g++-7

# Install OpenJDK-8
RUN apt-get update && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y ant && \
    apt-get clean;

# Fix certificate issues
RUN apt-get update && \
    apt-get install ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f;

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

# --- PIP UPDATE
RUN $CONDA_DIR/bin/python -m pip install --upgrade pip

# --- basemap
RUN apt-get install -y  libgeos-dev
# RUN apt-get install -y  libgeos
RUN $CONDA_DIR/bin/python -m pip install https://github.com/matplotlib/basemap/archive/master.zip


# --- Install h2o
RUN $CONDA_DIR/bin/python -m pip install -f http://h2o-release.s3.amazonaws.com/h2o/latest_stable_Py.html h2o
    # h2o (requires java)
    # requires java
# RUN wget --no-verbose http://h2o-release.s3.amazonaws.com/h2o/latest_stable -O latest && \
#     wget --no-verbose --no-check-certificate -i latest -O h2o.zip && rm latest && \
#     unzip h2o.zip && rm h2o.zip && cp h2o-*/h2o.jar . && \
#     $CONDA_DIR/bin/python -m pip install `find . -name "*whl"`
    
# ADD clean-layer.sh  /tmp/clean-layer.sh
# RUN /tmp/clean-layer.sh



# --- Install vowpalwabbit
# RUN $CONDA_DIR/bin/python -m  pip install --global-option="--vcpkg-root=path\to\vcpkg" vowpalwabbit
# RUN cd /usr/local/src && \
#    git clone -b 8.6.0 https://github.com/JohnLangford/vowpal_wabbit.git && \
#    ./vowpal_wabbit/python/conda_install.sh && \
#    # Reinstall in non-editable mode (without the -e flag)
#    pip install vowpal_wabbit/python
# --- TRY TO INSTALL NEW PACKAGES 
RUN $CONDA_DIR/bin/python -m pip install feather-format
RUN $CONDA_DIR/bin/python -m pip install skope-rules

# --- Conda xgboost, lightgbm, catboost, h2o, gensim, mlxtend
RUN conda install --quiet --yes \
    'boost' \
    'lightgbm' \
    'xgboost' \
    'catboost' \
    'gensim' \
    'mlxtend' \
    'tabulate' \
    'altair' \
    'vega3' \
    'vega' \
    'vega_datasets' \
    'featuretools' \
    'more-itertools' \
    'folium' \
    'mxnet' \
    'fbprophet' \
    'seaborn' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# -- 
RUN jupyter nbextension install --sys-prefix --py vega3
RUN $CONDA_DIR/bin/python -m pip install --upgrade jupyterlab

# --- Install hyperopt, tpot, sklearn-deap, yellowbrick, spacy
RUN $CONDA_DIR/bin/python -m pip install hyperopt \
					 deap \
					 update_checker \
					 tqdm \
					 stopit \
					 scikit-mdr \
					 skrebate \
					 tpot \
					 scikit-learn \
					 sklearn-deap \
					 yellowbrick \
					 spacy \
					 gplearn \
					 kmapper \
                                         skope-rules \
					 shap \
					 lime \
					 geojson \
					 descartes \
					 geopandas \
					 chart-studio \
					 viz 


###########
#
# Add some usefull libs, inspired by kaggle's Dockerfile
# CREDITS : https://hub.docker.com/r/kaggle/python/dockerfile
#
###########
#RUN $CONDA_DIR/bin/python -m pip install --upgrade mpld3
RUN $CONDA_DIR/bin/python -m pip install mplleaflet \
					 gpxpy \
					 arrow \
					 sexmachine \
					 Geohash \
					 haversine \
					 toolz cytoolz \
					 sacred \
					 plotly \
					 git+https://github.com/nicta/dora.git \
					 git+https://github.com/hyperopt/hyperopt.git \
# tflean. Deep learning library featuring a higher-level API for TensorFlow. http://tflearn.org
					 git+https://github.com/tflearn/tflearn.git \
					 fitter \
					 langid \
# Delorean. Useful for dealing with datetime
					 delorean \
					 trueskill \
					 heamy \
					 vida \
# Useful data exploration libraries (for missing data and generating reports)
					 missingno \
					 pandas-profiling \
					 s2sphere 
					 
RUN $CONDA_DIR/bin/python -m pip install vowpalwabbit==8.5.0

###########
#
# Issue #1
# pandas.read_hdf
#
###########
RUN $CONDA_DIR/bin/python -m pip install --upgrade tables

# --- update CONDA
# RUN conda update --all
# RUN pip freeze — local | grep -v ‘^\-e’ | cut -d = -f 1 | xargs -n1 pip install -U

# clean up pip cache
RUN rm -rf /root/.cache/pip/*

# Delete old downloaded archive files 
RUN apt-get autoremove -y
# Delete downloaded archive files
RUN apt-get clean
# Delete source files used for building binaries
RUN rm -rf /usr/local/src/*
# Delete conda downloaded tarballs
RUN conda clean -y --tarballs

