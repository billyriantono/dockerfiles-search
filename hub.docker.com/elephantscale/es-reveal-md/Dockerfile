FROM ubuntu:bionic

# args for docker file
ARG MYUSER=ubuntu
ARG HOME_DIR=/home/${MYUSER}
ARG CONDA_DIR=${HOME_DIR}/conda
ARG NVM_VERSION=0.34.0

# envs for the runtime container
ENV NVM_DIR         ${HOME_DIR}/nvm
ENV NODE_VERSION    10.15.2
ENV ES_HOME         ${HOME_DIR}
ENV WORKING_DIR     ${HOME_DIR}/dev
ENV NODE_PATH       ${NVM_DIR}/v${NODE_VERSION}/lib/node_modules
ENV PATH            ${NVM_DIR}/versions/node/v${NODE_VERSION}/bin:${PATH}

## for apt to be noninteractive
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true


RUN echo "*** http_proxy=${http_proxy} ***"

## update all system
RUN apt-get update --fix-missing -yq && \
    apt-get -yq upgrade

## basic utils
RUN apt-get update && apt-get install -yq  --no-install-recommends \
    atop \
    build-essential \
    ca-certificates \
    curl \
    git \
    less \
    #libssl-dev \
    jq \
    openssh-client \
    nano \
    rsync \
    screen \
    sudo \
    vim \
    unzip \
    wget \
    zip

## stuff for chromium
RUN apt-get update && apt-get install -yq \
        ca-certificates \
        fonts-liberation \
        gconf-service \
        gnupg \
        libappindicator1 \
        libasound2 \
        libatk1.0-0 \
        libc6 \
        libcairo2 \
        libcups2 \
        libdbus-1-3 \
        libexpat1 \
        libfontconfig1 \
        libgcc1 \
        libgconf-2-4 \
        libgdk-pixbuf2.0-0 \
        libglib2.0-0 \
        libgtk-3-0 \
        libnspr4 \
        libnss3 \
        libpango-1.0-0 \
        libpangocairo-1.0-0 \
        libstdc++6 \
        libx11-6 \
        libx11-xcb1 \
        libxcb1 \
        libxcomposite1 \
        libxcursor1 \
        libxdamage1 \
        libxext6 \
        libxfixes3 \
        libxi6 \
        libxrandr2 \
        libxrender1 \
        libxss1 \
        libxtst6 \
        lsb-release \
        ttf-bitstream-vera \
        ttf-dejavu \
        wget \
        xdg-utils

## For PdfLatex
RUN apt-get update && apt-get install -yq \
    texlive-latex-base texlive-fonts-recommended texlive-fonts-extra texlive-latex-extra

## done with all APT installs
## --- cleanup apt
RUN apt clean && \
        rm -rf /var/lib/apt/lists/*


## Adding a regular ubuntu user
RUN useradd -rm -d ${HOME_DIR} -s /bin/bash -g root -G sudo,audio,video -u 1000 ${MYUSER}

RUN echo "${MYUSER} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers


## ---------------- change to ubuntu user -------------
USER ${MYUSER}
WORKDIR ${HOME_DIR}


# Install nvm with node and npm
RUN mkdir -p ${NVM_DIR}
RUN curl https://raw.githubusercontent.com/creationix/nvm/v${NVM_VERSION}/install.sh | bash \
    && . ${NVM_DIR}/nvm.sh \
    && nvm install ${NODE_VERSION} \
    && nvm alias default ${NODE_VERSION} \
    && nvm use default


## Install npm latest version
RUN  npm -g install npm

## install reveal-md by forcing to install puppeteer & Chromium
## following are for installing specific tags / branches
RUN npm i -g -f elephantscale/es-reveal-md#r-es-prod
# RUN npm i -g -f elephantscale/es-reveal-md
#RUN npm i -g -f git://github.com/elephantscale/es-reveal-md#dev


## install miniconda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.12-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p ${CONDA_DIR} && \
    rm ~/miniconda.sh && \
#    ${CONDA_DIR}/bin/conda clean -tipsy && \
    echo ". ${CONDA_DIR}/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

## install python packages
RUN ${CONDA_DIR}/bin/conda install \
        beautifulsoup4 \
        matplotlib \
        pandoc  \
        pillow \
        pygments 

## install python packages using pip
RUN ${CONDA_DIR}/bin/pip install \
        anytree \
        mistletoe \
        pytablewriter \
        python-pptx


## work dir - this is where the slides would be mounted
RUN mkdir -p ${WORKING_DIR}

## setup SSH deploy key for github
RUN mkdir -p ${HOME_DIR}/.ssh/
COPY ssh-config-ubuntu   ${HOME_DIR}/.ssh/config
COPY deploy-utils.pem  ${HOME_DIR}/.ssh/
COPY deploy-utils.pub  ${HOME_DIR}/.ssh/
# do ssh-keyscan so github connection will work
RUN touch ${HOME_DIR}/.ssh/known_hosts
RUN ssh-keyscan github.com >> ${HOME_DIR}/.ssh/known_hosts
RUN sudo chown -R ${MYUSER}  ${HOME_DIR}/.ssh  && \
    chmod 600  ${HOME_DIR}/.ssh/*


## Clone utils repo
RUN  cd  ${HOME_DIR} && \
     git clone git@github.com:elephantscale/utils.git && \
     cd ${HOME_DIR}/utils && git checkout r-reveal-prod && \
     sudo chown -R ${MYUSER}  $HOME_DIR/utils

## Set prompt in bashrc
RUN echo 'export PS1="\e[0;31m\u@es-reveal-md  \[\w\] > \e[m "' >> ~/.bashrc

COPY ./startup.sh  $HOME_DIR/
RUN sudo chown ${MYUSER}  $HOME_DIR/*
#RUN sudo chown -R ${MYUSER}  $HOME_DIR
RUN sudo chmod +x  $HOME_DIR/*.sh


USER ${MYUSER}


#ENTRYPOINT ["./startup.sh"]
ENTRYPOINT ["/bin/bash", "/home/ubuntu/startup.sh"]
#CMD ["bash"]
