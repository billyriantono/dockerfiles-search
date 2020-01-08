FROM ubuntu:18.04
LABEL maintainer "dada"

# args
ARG USER='devuser'
ARG HOME='/home/'${USER}

# apt-get
ENV DEBIAN_FRONTEND=noninteractive
RUN sed -i.bak -e "s%http://archive.ubuntu.com/ubuntu/%http://jp.archive.ubuntu.com/ubuntu/%g" /etc/apt/sources.list
RUN apt-get update && \
    apt-get install -y git curl wget build-essential libbz2-dev libdb-dev \
    libreadline-dev libffi-dev libgdbm-dev liblzma-dev language-pack-ja-base language-pack-ja \
    libncursesw5-dev libsqlite3-dev libssl-dev unzip sudo fontconfig \
    zlib1g-dev uuid-dev tk-dev python2.7-dev python3-dev && \
    apt-get clean

RUN mkdir -p /tmp
WORKDIR /tmp

# gcloud install
RUN echo "deb http://packages.cloud.google.com/apt cloud-sdk-bionic main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
	curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - && \
	sudo apt update && sudo apt install -y google-cloud-sdk google-cloud-sdk-app-engine-python google-cloud-sdk-app-engine-python-extras kubectl

# terraform インストール
RUN wget https://releases.hashicorp.com/terraform/0.12.4/terraform_0.12.4_linux_amd64.zip
RUN unzip terraform_0.12.4_linux_amd64.zip
RUN mv terraform /usr/bin/

RUN rm -rf /tmp/*

# 作業用ユーザ作成
RUN useradd -m ${USER} && \
    echo "${USER} ALL=(ALL) ALL" > /etc/sudoers.d/${USER} && \
    echo "${USER}:${USER}" | chpasswd && \
    mkdir /home/${USER}/.ssh && \
    chown -R ${USER}:${USER} /home/${USER}/.ssh && \
    mkdir /home/${USER}/workspace && \
    chown -R ${USER}:${USER} /home/${USER}/workspace

# dotfiles install
WORKDIR ${HOME}
RUN git clone -b master --depth 1 \
    https://github.com/extdada/dotfiles.git && \
    /home/${USER}/dotfiles/setting.sh && \
    /home/${USER}/dotfiles/font.sh
RUN echo "alias vi='nvim'" >> ${HOME}/.bashrc && \
    echo "alias vim='nvim'" >> ${HOME}/.bashrc

RUN locale-gen ja_JP.UTF-8 && \
    echo "export LANG=ja_JP.UTF-8" >> ${HOME}/.bashrc

RUN chown -R ${USER}:${USER} ${HOME}

# user setting
USER ${USER}

# bash
CMD ["/bin/bash"]
