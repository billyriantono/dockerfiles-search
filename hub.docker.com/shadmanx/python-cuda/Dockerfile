FROM nvidia/cuda:10.1-devel

ARG CONDA_VERSION="3-2019.07"
ARG CONDA_PATH="/root/anaconda"

ENV PATH="${CONDA_PATH}/bin:${PATH}"

RUN apt-get update \
 && apt-get install -y curl \
    # download and install anaconda
 && curl -O https://repo.anaconda.com/archive/Anaconda${CONDA_VERSION}-Linux-x86_64.sh \
 && sh Anaconda${CONDA_VERSION}-Linux-x86_64.sh -b -p ${CONDA_PATH} \
 && rm Anaconda${CONDA_VERSION}-Linux-x86_64.sh \
    # install all python packages
 && conda install -y -c anaconda cudatoolkit=10.1 \
 && conda install -y -c conda-forge scikit-learn graphviz python-graphviz bcolz pyhamcrest pandas tensorflow \
 && conda install -y -c pytorch pytorch torchvision \
    # clean up
 && conda clean -y -a \
 && apt-get purge -y curl \
 && apt-get -y autoremove \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# SUCCEEDS

# UNTESTED
# RUN conda update -n base conda
# RUN conda update --all
# RUN conda install -c creditx sklearn-pandas
# RUN conda install -c chubb-gregory_werbin sklearn-pandas
#RUN conda install -c conda-forge pandas
#RUN pip install isoweek
#RUN pip install sklearn-pandas
#RUN conda install -c conda-forge pandas-summary
#RUN pip install torchtext
#RUN pip install torch torchvision
# RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y cuda-drivers

# FAILS
#RUN conda install -y -c conda-forge opencv
#RUN conda install -y -c auto isoweek
