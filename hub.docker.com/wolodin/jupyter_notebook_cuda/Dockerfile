# ==================================================================
# module list
# ------------------------------------------------------------------
# Miniconda3-4.7.12.1  (wget)
# progressbar2  latest (pip)
# pytorch  latest (conda)
# torchvision  latest (conda)
# cudatoolkit  10.0 (conda)
# ipython  latest (conda)
# numpy  latest (conda)
# pandas  latest (conda)
# scikit-learn  latest (conda)
# notebook  latest (conda)
# matplotlib  latest (conda)
# scikit-image latest (conda)
# ==================================================================
ARG BASEIMAGE_VERION=9.2-devel-ubuntu18.04
FROM nvidia/cuda:${BASEIMAGE_VERION} as jupyter_notebook_cuda

LABEL maintainer="Volodin Vasiliy <wolodin@vvp24.ru>" \
      version="1.3.2" \
      name="jupyter_notebook_cuda"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV DATA_MAPPING_USERNAME_ENV="data-mapping"
ENV MINICONDA_URL_PACKAGE_ENV="https://repo.continuum.io/miniconda/Miniconda3-4.7.12.1-Linux-x86_64.sh"

RUN groupadd ${DATA_MAPPING_USERNAME_ENV} && \
    useradd -d /home/${DATA_MAPPING_USERNAME_ENV} -ms /bin/bash -g ${DATA_MAPPING_USERNAME_ENV} -G sudo ${DATA_MAPPING_USERNAME_ENV}

RUN APT_INSTALL="apt-get install -qq --no-install-recommends" && \
    apt-get update --fix-missing -qq && apt-get upgrade -qq && \
    # ==================================================================
    # tools
    # ------------------------------------------------------------------
        DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
            locales \
            apt-utils \
            software-properties-common \
            && \
        localedef -i ru_RU -c -f UTF-8 -A /usr/share/locale/locale.alias ru_RU.UTF-8 \
            && \
        DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
            ca-certificates \
            git mercurial subversion \
            nano sed \
            libssl1.0.0 libssl-dev \
            curl wget \
            grep dpkg \
            inetutils-ping \
            tmux man htop mc \
            tar gzip bzip2 zip unzip rar unrar \
            libglib2.0-0 libxext6 libsm6 libxrender1 \
            && \
        # ==================================================================
        # config & cleanup
        # ------------------------------------------------------------------
            ldconfig && \
            apt-get clean && \
            apt-get autoremove -qq && \
            rm -rf /var/lib/apt/lists/* /tmp/* ~/*

ENV LANG=ru_RU.UTF-8 LC_ALL=ru_RU.UTF-8

# ==================================================================
# miniconda
# ------------------------------------------------------------------
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet ${MINICONDA_URL_PACKAGE_ENV} -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

ENV PATH /opt/conda/bin:$PATH
# ==================================================================
# pytorch torchvision cudatoolkit=10.0
# ipython numpy pandas scikit-learn notebook matplotlib
# scikit-image
# ------------------------------------------------------------------
RUN CONDA_INSTALL="conda install -y --update-deps" && \
        conda update conda && \
        $CONDA_INSTALL \
        pytorch torchvision cudatoolkit=10.0 -c pytorch && \
        #pytorch-cpu torchvision-cpu -c pytorch
        $CONDA_INSTALL \
        ipython numpy pandas scikit-learn notebook matplotlib \
        scikit-image \
        && \
        conda clean -a

RUN PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    $PIP_INSTALL progressbar2

# ==================================================================
# config & cleanup
# ------------------------------------------------------------------
RUN ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/*

USER ${DATA_MAPPING_USERNAME_ENV}:${DATA_MAPPING_USERNAME_ENV}

WORKDIR /home/${DATA_MAPPING_USERNAME_ENV}

RUN jupyter notebook --generate-config && \
	echo "c.NotebookApp.ip = '0.0.0.0'" >> ~/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.allow_origin = '*'" >> ~/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.password = u'sha1:3379fd89793c:4dfb6fd74c64a436b43f30dd33e9a3a68433ce52'" >> ~/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.open_browser = False" >> ~/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.allow_remote_access = True" >> ~/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.port = 8765" >> ~/.jupyter/jupyter_notebook_config.py

EXPOSE 8765

ENTRYPOINT ["jupyter", "notebook", "--no-browser", "--port 8765"]

#HEALTHCHECK --timeout=10s CMD curl --silent --fail http://127.0.0.1:8765/
