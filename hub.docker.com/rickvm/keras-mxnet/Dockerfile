#Base image that supplies us with an anaconda3 installation (and jupyteR)
FROM continuumio/anaconda3:5.0.1

 # Use a fixed apt-get repo to stop intermittent failures due to flaky httpredir connections,
    # as described by Lionel Chan at http://stackoverflow.com/a/37426929/5881346
RUN sed -i "s/httpredir.debian.org/debian.uchicago.edu/" /etc/apt/sources.list && \
    apt-get update && apt-get install -y build-essential && \
    # https://stackoverflow.com/a/46498173
    conda update -y conda && conda update -y python
	
RUN apt-get install -y libfreetype6-dev && \
    apt-get install -y libglib2.0-0 libxext6 libsm6 libxrender1 libfontconfig1 --fix-missing && \
	#keras
    cd /usr/local/src && \
	mkdir keras && cd keras && \
    git clone --depth 1 https://github.com/dmlc/keras/ && \
    cd keras && python setup.py install && \
    #clean up
    rm -rf /root/.cache/pip/* && \
    apt-get autoremove -y && apt-get clean && \
    rm -rf /usr/local/src/*
	
# Make sure the dynamic linker finds the right libstdc++
ENV LD_LIBRARY_PATH=/opt/conda/lib

RUN apt-get update && \
	# MXNet
    pip install mxnet && \
	# Keras setup
    # Keras likes to add a config file in a custom directory when it's
    # first imported. This doesn't work with our read-only filesystem, so we
    # have it done now
    python -c "from keras.models import Sequential"  && \
    # Switch to TF backend
    sed -i 's/theano/tensorflow/' /root/.keras/keras.json  && \
    # Re-run it to flush any more disk writes
    python -c "from keras.models import Sequential; from keras import backend; print(backend._BACKEND)" && \
    # Keras reverts to /tmp from ~ when it detects a read-only file system
    mkdir -p /tmp/.keras && cp /root/.keras/keras.json /tmp/.keras && \
    # Scikit-Learn nightly build
    cd /usr/local/src && git clone https://github.com/scikit-learn/scikit-learn.git && \
    cd scikit-learn && python setup.py build && python setup.py install
	
RUN pip install --upgrade mpld3 && \
	pip install pandas-profiling && \
    pip install git+https://github.com/hyperopt/hyperopt.git && \
	pip install sklearn-pandas && \
	# Update setuptools and add tensorpack
    pip install --upgrade --ignore-installed setuptools && pip install --no-cache-dir git+git://github.com/ppwwyyxx/tensorpack && \
	pip install pandas-datareader && \
	# clean up pip cache
    rm -rf /root/.cache/pip/*
	
#Temporary fixes
    # Stop Matplotlib printing junk to the console on first load
	RUN sed -i "s/^.*Matplotlib is building the font cache using fc-list.*$/# Warning removed by Kaggle/g" /opt/conda/lib/python3.6/site-packages/matplotlib/font_manager.py && \
    # Make matplotlib output in Jupyter notebooks display correctly
    mkdir -p /etc/ipython/ && echo "c = get_config(); c.IPKernelApp.matplotlib = 'inline'" > /etc/ipython/ipython_config.py
	
# Set backend for matplotlib
ENV MPLBACKEND "agg"
