FROM ubuntu:16.04

MAINTAINER Arjun Sreekumar <ajsrk1207@gmail.com>

# PyTorch Dependencies - 
# 	1.  build-essential 
#       2.  cmake 
#       3.  git 
#       4.  curl 
#       5.  vim 
#       6.  ca-certificates 
#       7.  libnccl2=2.0.5-2+cuda8.0 
#       8.  libnccl-dev=2.0.5-2+cuda8.0 
#       9.  libjpeg-dev 
#       10. libpng-dev 
#       11. conda install - numpy pyyaml scipy ipython mkl
#       12. conda install -c pytorch pytorch torchvision magma-cuda80
# Tensorflow Dependencies - 
#       1. build-essential 
#       2. curl 
#       3. libfreetype6-dev 
#       4. libpng12-dev 
#       5. libzmq3-dev 
#       6. pkg-config 
#       7. python 
#       8. python-dev 
#       9. rsync 
#       10. software-properties-common 
#       11. unzip 
#       12. conda install pip jupyter Pillow h5py ipykernel
#       13. conda install -c conda-forge matplotlib numpy pandas scipy
# Mayavi Dependencies - 
#       1. mesa-utils
#       2. libglu1-mesa
#       3. libqtgui4

#ARG MINICONDA_VERSION=Miniconda3-4.5.4-Linux-x86_64.sh
ARG MINICONDA_VERSION=Miniconda3-4.7.10-Linux-x86_64.sh

ARG VSCODE_PYTHON_EXTENSION_VERSION=2019.6.22090

ARG UID=1000

ARG GID=1000

ENV LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 LANGUAGE=en_US.UTF-8

ENV PATH /opt/conda/bin:$PATH

ENV HOME /home

ENV PYCHARM_HOME=/etc/pycharm

ENV PYCHARM=/etc/pycharm/bin/pycharm.sh

EXPOSE 8888

ADD . /

RUN apt-get update --fix-missing && \
   apt-get install -y --no-install-recommends --allow-downgrades wget bzip2 ca-certificates \
   mesa-utils libglu1-mesa libqtgui4 \
   git \
   build-essential cmake curl vim ca-certificates \
   libjpeg-dev libpng12-dev \
   libfreetype6-dev libzmq3-dev pkg-config python-dev rsync software-properties-common unzip libxtst6 \
   locales \
   sudo &&\
   locale-gen en_US.UTF-8

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/${MINICONDA_VERSION} -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh &&\
    \
    apt-get clean

    #RUN conda config --add pinned_packages defaults::conda && \
RUN conda config --add channels conda-forge && \
    conda update -n base conda && \
    while read requirement; do conda install --yes -c conda-forge $requirement; done < conda_forge_requirements.txt && \
    while read requirement; do conda install --yes -c pytorch $requirement; done < pytorch_requirements.txt && \
    pip install tensorflow && \
    pip install pycocotools==2.0.0 &&\
    pip install torchsummary &&\
    wget https://download.jetbrains.com/python/pycharm-community-2018.2.tar.gz -O /tmp/pycharm.tar.gz &&\
    mkdir ${PYCHARM_HOME} && tar -xzvf /tmp/pycharm.tar.gz -C ${PYCHARM_HOME} --strip=1 && \
    echo 'alias pycharm="/etc/pycharm/bin/pycharm.sh"' >> ~/.bashrc && \
    rm -rf /var/lib/apt-lists; rm -rf /tmp/*; apt-get purge wget -y; apt-get autoremove -y

# Code-Server
# Dependencies - bsdstar, openssl, locales, net-tools 
RUN apt-get update && apt-get install --no-install-recommends -y \
    bsdtar \
    openssl \
    net-tools \
    && rm -rf /var/lib/apt/lists/*

RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LANG en_US.utf8
ENV DISABLE_TELEMETRY true

#ENV CODE_VERSION="1.1119-vsc1.33.1"
ENV CODE_VERSION="1.1156-vsc1.33.1"

RUN curl -sL https://github.com/cdr/code-server/releases/download/${CODE_VERSION}/code-server${CODE_VERSION}-linux-x64.tar.gz | tar --strip-components=1 -zx -C /usr/local/bin code-server${CODE_VERSION}-linux-x64/code-server


# Setup User
RUN groupadd -g $GID -r coder \
    && useradd -m -r coder -u $UID -g coder -s /bin/bash \
    && echo "coder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/nopasswd


USER coder

ENV HOME /home/coder


COPY jupyter_notebook_config.py ~/.jupyter/jupyter_notebook_config.py

# Setup User Visual Studio Code Extentions
ENV VSCODE_USER "/home/coder/.local/share/code-server/User"
ENV VSCODE_EXTENSIONS "/home/coder/.local/share/code-server/extensions"

RUN mkdir -p ${VSCODE_USER}
COPY --chown=coder:coder settings.json /home/coder/.local/share/code-server/User/

# Setup Python Extension
RUN mkdir -p ${VSCODE_EXTENSIONS}/python \
    && curl -JLs --retry 5 https://marketplace.visualstudio.com/_apis/public/gallery/publishers/ms-python/vsextensions/python/${VSCODE_PYTHON_EXTENSION_VERSION}/vspackage | bsdtar --strip-components=1 -xf - -C ${VSCODE_EXTENSIONS}/python extension

# Setup User Workspace
RUN mkdir -p /home/coder/project
WORKDIR /home/coder/project

#ENTRYPOINT ["dumb-init", "code-server"]

CMD [ "/bin/bash" ]

#ENTRYPOINT ["/etc/pycharm/bin/pycharm.sh"]

