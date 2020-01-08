# Start with anaconda image
FROM continuumio/anaconda3

LABEL version="0.0.2"
LABEL imagename="ml-base"

WORKDIR /

# Make bash the default shell
SHELL ["/bin/bash", "-c"]

RUN conda update -y conda
RUN conda config --add channels conda-forge
RUN conda update -y pip

# Make sure the conda bin is in the path
ENV PATH /opt/conda/bin:$PATH

# install basic ML and DS tools
RUN conda install --yes python=3.6 tensorflow pytorch tensorboard numpy matplotlib pandas jupyter scipy

# For Tensorboard
EXPOSE 6006
# On host start container with '-p 0.0.0.0:6006:6006' option.
# This will map the port correctly in the container.
# In container: tensorboard --logdir=<logdir>
# Connect on host browser via: localhost:6006

# For Jupyter
EXPOSE 8888
# Copy shortcut command for starting jupyter notebook
COPY start-jupyter.sh /usr/local/bin
RUN chmod a+x /usr/local/bin/start-jupyter.sh
# On host start container with '-p 0.0.0.0:8888:8888'.
# This will map the port correctly in the container.
# On container cd into desired dir and run start-jupyter.sh.
# Connect on host browser via: 'http://localhost:8888/?token=<token output from running command>​'




