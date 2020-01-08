FROM spacemacs/emacs25:develop

MAINTAINER tom <273412935@qq.com>

## - traceroute, telnet, gvm-tools,  -
RUN apt-get update && apt-get install \
    apt-utils \
    curl \
    rlwrap \
    silversearcher-ag \
    wget \
    zsh \
    telnet \
    traceroute \
    tree \
    python3-pip \
    python-pip \
    privoxy \
    git \
    mercurial \
    make \
    binutils \
    bison \
    gcc \
    build-essential

## - python, pip3, virtualenvwrapper -
RUN pip install virtualenv \
    virtualenvwrapper \
    && pip3 install virtualenv \
    virtualenvwrapper

## - vim -
RUN apt-get remove vim-common && apt-get install vim

## - nodejs -
RUN /bin/sh -c "curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -" \
    && apt-get update \
    && apt-get install \
    nodejs

## - golang -
#RUN wget https://dl.google.com/go/go1.11.4.linux-amd64.tar.gz
#RUN tar -C /usr/local -xzf go1.11.4.linux-amd64.tar.gz \
#    rm ./go1.11.4.linux-amd64.tar.gz
RUN wget -P /tmp/ https://studygolang.com/dl/golang/go1.11.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf /tmp/go1.11.linux-amd64.tar.gz \
    && rm /tmp/go1.11.linux-amd64.tar.gz

## - hugo -
RUN wget -P /tmp/ https://github.com/gohugoio/hugo/releases/download/v0.52/hugo_0.52_Linux-64bit.tar.gz \
    && tar -C /tmp/ -zxf /tmp/hugo_0.52_Linux-64bit.tar.gz \
    && ls /tmp/ \
    && rm /tmp/LICENSE /tmp/README.md \
    && mv /tmp/hugo /usr/local/bin/

## - chrome -
#RUN wget -q -O - "${CHROME_KEY}" | apt-key add - \
#    && echo "${CHROME_REP}" >> /etc/apt/sources.list.d/google.list \
#    && apt-get update \
#    && apt-get install 	google-chrome-stable \
#    && rm -rf /tmp/* /var/lib/apt/lists/* \
#    && google-chrome \
#    --disable-gpu \
#    --headless \
#    --no-sandbox \
#    https://example.org/

# COPY .lein "${UHOME}/.lein"
#RUN echo "(defproject stub \"0.0.1-SNAPSHOT\")" > /tmp/project.clj \
#    && cd /tmp/ \
#    && lein deps \
#    && rm -rf /tmp/*

ENV CHROME_KEY="https://dl-ssl.google.com/linux/linux_signing_key.pub" \
    CHROME_REP="deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main"

ENV UNAME="tom"
# prepare spacemacs configuration

#RUN git submodule init
#RUN git submodule update
COPY spacemacs/zilongshanren-tomtsang/target/latest/spacemacs-private/ "${UHOME}/.spacemacs.d/"
RUN /bin/sh -c "ls -l ${UHOME}/.spacemacs.d/ && echo ${UHOME}"

# Install Spacemacs layers dependencies and init user
RUN mv ${UHOME}/.spacemacs ${UHOME}/.spacemacs.bak
RUN install-deps ; exit 0;

RUN echo 'This is OK'

## change to $UNAME ###############################################

USER $UNAME

RUN git config --global user.name tom \
    && git config --global user.email 273412935@qq.com

## - gvm -
RUN wget https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer \
    && /bin/sh -c "chmod +x ./gvm-installer && ./gvm-installer"

## - oh-my-zsh -
RUN sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"; exit 0;
ENV WORKON_HOME ${UHOME}/.virtualenvs
RUN mkdir -p $WORKON_HOME
#RUN /bin/sh -c "which zsh"


## change to root #################################################
USER root

## - dotfiles -
COPY dotfiles/.gitconfig "${UHOME}/.gitconfig"
COPY dotfiles/ubuntu/ "${UHOME}/ubuntu/"

## - config $UNAME zshrc - 
RUN /bin/sh -c "cat ${UHOME}/ubuntu/zshrc.txt >> ${UHOME}/.zshrc"

## change to root #################################################
USER root
