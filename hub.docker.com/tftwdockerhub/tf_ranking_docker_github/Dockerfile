# Author: Teng Fu
# Contact: teng.fu@teleware.com
# This Dockerfile includes following features:
# 1. based on latest-gpu-py3 tensorflow docker image
# 2. jupyter installed
# 3. jupyter extension installed
# 4. TensorFlow-Ranking installed

FROM tensorflow/tensorflow:latest-gpu-py3 

# COPY the pip package into root directory
COPY ./tf_ranking_pip/tensorflow_ranking-0.1.0-py2.py3-none-any.whl /

WORKDIR /

RUN pip --no-cache-dir install \
    jupyter \
    tensorflow_ranking-0.1.0-py2.py3-none-any.whl

# Set up our notebook config.
COPY jupyter_notebook_config.py /root/.jupyter/

# Jupyter has issues with being run directly:
#   https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY run_jupyter.sh /

# the default volume shared with host machine directory
# in the docker run 
# use docker run -v <absolute path of local folder>:/app
RUN mkdir /app

WORKDIR /app

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

# automatic run this bash file 
# because it is currently installed with anaconda, so must specified the bash's path
CMD [ "/bin/bash", "/run_jupyter.sh", "--allow-root"]