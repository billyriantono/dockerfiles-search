FROM ubuntu:16.04

################################## JUPYTERLAB ##################################

ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

RUN apt-get -o Acquire::ForceIPv4=true update && apt-get -yq dist-upgrade \
 && apt-get -o Acquire::ForceIPv4=true install -yq --no-install-recommends \
	locales cmake git build-essential \
    python-pip \
	python3-pip python3-setuptools \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip setuptools \
 && python3 -m pip install jupyterlab==0.35.4 bash_kernel==0.7.1 tornado==5.1.1 \
 && python3 -m bash_kernel.install

ENV SHELL=/bin/bash \
	NB_USER=jovyan \
	NB_UID=1000 \
	LANG=en_US.UTF-8 \
	LANGUAGE=en_US.UTF-8

ENV HOME=/home/${NB_USER}

RUN adduser --disabled-password \
	--gecos "Default user" \
	--uid ${NB_UID} \
	${NB_USER}

EXPOSE 8888

CMD ["jupyter", "lab", "--no-browser", "--ip=0.0.0.0", "--NotebookApp.token=''"]

##################################### APT ######################################

RUN apt-get -o Acquire::ForceIPv4=true update \
 && apt-get -o Acquire::ForceIPv4=true install -yq --no-install-recommends \
    python-setuptools \
    python-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

##################################### PIP ######################################

RUN pip2 install --upgrade pip

RUN pip2 install  \
    tensorflow==1.4 \
    matplotlib==2.2.3 \
    numpy==1.14 \
    scipy==0.19.1 \
    ipython==5.8.0 \
    ipykernel==4.10.0 \
    tornado==5.1.1 \
    googledrivedownloader \
    requests \
    gensim

##################################### COPY #####################################

RUN mkdir ${HOME}/text2action

COPY . ${HOME}/text2action

################################### CUSTOM #####################################

RUN python2 -m ipykernel install

##################################### TAIL #####################################

RUN chown -R ${NB_UID} ${HOME}

USER ${NB_USER}

WORKDIR ${HOME}/text2action
