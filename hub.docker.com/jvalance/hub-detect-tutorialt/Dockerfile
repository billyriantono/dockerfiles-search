# Generated by Neurodocker version 0.4.3-dev
# Timestamp: 2018-11-13 18:59:40 UTC
#
# Thank you for using Neurodocker. If you discover any issues
# or ways to improve this software, please submit an issue or
# pull request on our GitHub repository:
#
#     https://github.com/kaczmarj/neurodocker

FROM debian:stretch

ARG DEBIAN_FRONTEND="noninteractive"

ENV LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    ND_ENTRYPOINT="/neurodocker/startup.sh"
RUN export ND_ENTRYPOINT="/neurodocker/startup.sh" \
    && apt-get update -qq \
    && apt-get install -y -q --no-install-recommends \
           apt-utils \
           bzip2 \
           ca-certificates \
           curl \
           locales \
           unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && dpkg-reconfigure --frontend=noninteractive locales \
    && update-locale LANG="en_US.UTF-8" \
    && chmod 777 /opt && chmod a+s /opt \
    && mkdir -p /neurodocker \
    && if [ ! -f "$ND_ENTRYPOINT" ]; then \
         echo '#!/usr/bin/env bash' >> "$ND_ENTRYPOINT" \
    &&   echo 'set -e' >> "$ND_ENTRYPOINT" \
    &&   echo 'if [ -n "$1" ]; then "$@"; else /usr/bin/env bash; fi' >> "$ND_ENTRYPOINT"; \
    fi \
    && chmod -R 777 /neurodocker && chmod a+s /neurodocker

ENTRYPOINT ["/neurodocker/startup.sh"]

RUN apt-get update -qq \
    && apt-get install -y -q --no-install-recommends \
           gcc \
           g++ \
           graphviz \
           tree \
           bsdtar \
           git \
           vim \
           emacs-nox \
           nano \
           less \
           ncdu \
           tig \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN export tar='bsdtar'

ENV CONDA_DIR="/opt/miniconda-latest" \
    PATH="/opt/miniconda-latest/bin:$PATH"
RUN export PATH="/opt/miniconda-latest/bin:$PATH" \
    && echo "Downloading Miniconda installer ..." \
    && conda_installer="/tmp/miniconda.sh" \
    && curl -fsSL --retry 5 -o "$conda_installer" https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && bash "$conda_installer" -b -p /opt/miniconda-latest \
    && rm -f "$conda_installer" \
    && conda update -yq -nbase conda \
    && conda config --system --prepend channels conda-forge \
    && conda config --system --set auto_update_conda false \
    && conda config --system --set show_channel_urls true \
    && sync && conda clean -tipsy && sync \
    && conda create -y -q --name py35 \
    && conda install -y -q --name py35 \
           'python=3.5' \
           'jupyter' \
           'jupyterlab' \
           'jupyter_contrib_nbextensions' \
           'traits' \
           'pandas' \
           'matplotlib' \
           'scikit-learn' \
           'seaborn' \
           'mkl' \
           'mkl-service' \
           'nose' \
           'sphinx' \
           'theano' \
           'pygpu' \
    && sync && conda clean -tipsy && sync \
    && bash -c "source activate py35 \
    &&   pip install --no-cache-dir  \
             'https://github.com/nipy/nipype/tarball/master' \
             'https://github.com/INCF/pybids/tarball/master' \
             'nltools' \
             'nilearn' \
             'datalad[full]' \
             'nipy' \
             'duecredit' \
             'niwidgets' \
             'mne' \
             'deepdish' \
             'hypertools' \
             'ipywidgets' \
             'pynv' \
             'six' \
             'nibabel' \
             'joblib' \
             'parameterized' \
             'git+https://github.com/pymc-devs/pymc3' \
             'git+https://github.com/PsychoinformaticsLab/nipymc'" \
    && rm -rf ~/.cache/pip/* \
    && sync \
    && sed -i '$isource activate py35' $ND_ENTRYPOINT

RUN echo '{ \
    \n  "pkg_manager": "apt", \
    \n  "instructions": [ \
    \n    [ \
    \n      "base", \
    \n      "debian:stretch" \
    \n    ], \
    \n    [ \
    \n      "install", \
    \n      [ \
    \n        "gcc", \
    \n        "g++", \
    \n        "graphviz", \
    \n        "tree", \
    \n        "bsdtar", \
    \n        "git", \
    \n        "vim", \
    \n        "emacs-nox", \
    \n        "nano", \
    \n        "less", \
    \n        "ncdu", \
    \n        "tig" \
    \n      ] \
    \n    ], \
    \n    [ \
    \n      "run", \
    \n      "export tar='"'"'bsdtar'"'"'" \
    \n    ], \
    \n    [ \
    \n      "miniconda", \
    \n      { \
    \n        "create_env": "py35", \
    \n        "conda_install": [ \
    \n          "python=3.5", \
    \n          "jupyter", \
    \n          "jupyterlab", \
    \n          "jupyter_contrib_nbextensions", \
    \n          "traits", \
    \n          "pandas", \
    \n          "matplotlib", \
    \n          "scikit-learn", \
    \n          "seaborn", \
    \n          "mkl", \
    \n          "mkl-service", \
    \n          "nose", \
    \n          "sphinx", \
    \n          "theano", \
    \n          "pygpu" \
    \n        ], \
    \n        "pip_install": [ \
    \n          "https://github.com/nipy/nipype/tarball/master", \
    \n          "https://github.com/INCF/pybids/tarball/master", \
    \n          "nltools", \
    \n          "nilearn", \
    \n          "datalad[full]", \
    \n          "nipy", \
    \n          "duecredit", \
    \n          "niwidgets", \
    \n          "mne", \
    \n          "deepdish", \
    \n          "hypertools", \
    \n          "ipywidgets", \
    \n          "pynv", \
    \n          "six", \
    \n          "nibabel", \
    \n          "joblib", \
    \n          "parameterized", \
    \n          "git+https://github.com/pymc-devs/pymc3", \
    \n          "git+https://github.com/PsychoinformaticsLab/nipymc" \
    \n        ], \
    \n        "activate": true \
    \n      } \
    \n    ] \
    \n  ] \
    \n}' > /neurodocker/neurodocker_specs.json
