FROM phusion/baseimage:latest

##############################################################################
# change repo to mirrors.aliyun.com
##############################################################################
RUN set -x \
        && mv /etc/apt/sources.list /etc/apt/sources.list.bak \
        && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse' >> /etc/apt/sources.list \
        && echo 'deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse' >> /etc/apt/sources.list \
        && apt-get -qq update

##############################################################################
# create user
##############################################################################
RUN set -x \
    && useradd --create-home --shell /bin/bash glzhao

##############################################################################
# base image
##############################################################################
RUN set -x \
        && apt-get -qq install apt-utils sudo \
        && apt-get install -qqy tmux irssi gnupg openssh-server \
        && apt-get install -qqy git vim cscope cgvg subversion ack-grep exuberant-ctags \
        && apt-get install -qqy python-pip ipython

USER glzhao
RUN set -x \
        && mkdir -p /home/glzhao/repos/config \
        && git clone https://github.com/glzhao/config.git /home/glzhao/repos/config/

RUN set -x \
        && ln -sf /home/glzhao/repos/config/_alias /home/glzhao/.alias \
        && ln -sf /home/glzhao/repos/config/_bashrc /home/glzhao/.bashrc \
        && ln -sf /home/glzhao/repos/config/_bashrc.addon /home/glzhao/.bashrc.addon \
        && ln -sf /home/glzhao/repos/config/_tmux.conf /home/glzhao/.bashrc.addon \
        && ln -sf /home/glzhao/repos/config/_bin /home/glzhao/.bin \
        && ln -sf /home/glzhao/repos/config/_gitconfig /home/glzhao/.gitconfig \
        && ln -sf /home/glzhao/repos/config/_git-prompt.sh /home/glzhao/.git-prompt.sh \
        && ln -sf /home/glzhao/repos/config/_git-completion.bash /home/glzhao/.git-completion.bash

##############################################################################
# golang
##############################################################################
USER root
RUN apt-get install -qqy golang

#USER glzhao
##############################################################################
# vim
##############################################################################
USER root
RUN set -x \
        && apt-get install -qqy software-properties-common wget curl man unzip nano colord rsync \
        && apt-get install -qqy make cmake clang build-essential python-dev python3-dev

USER glzhao
RUN set -x \
        && ln -sf /home/glzhao/repos/config/_vimrc /home/glzhao/.vimrc  \
        && ln -sf /home/glzhao/repos/config/_ycm_extra_conf.py /home/glzhao/.ycm_extra_conf.py

RUN set -x \
        && vim -E -u /home/glzhao/.vimrc -S ~/.vim/vundle.vim +PluginInstall +qall || true
        #&& vim -u /home/glzhao/repos/config/_vimrc +PluginInstall +qall -c q -c q
        #&& vim +GoInstallBinaries +qall -c q -c q

RUN cd ~/.vim/bundle/YouCompleteMe/ \
        && git submodule update --init --recursive \
        && ./install.py --clang-completer --gocode-completer

##############################################################################
# zsh
##############################################################################
USER root
RUN set -x \
        && apt-get install -qqy zsh autojump \
        && chsh -s /bin/zsh glzhao

USER glzhao
RUN set -x \
        && cd /home/glzhao/repos/config/ && git submodule update --init --recursive

RUN set -x \
        && ln -s /home/glzhao/repos/config/_zshrc /home/glzhao/.zshrc \
        && ln -s /home/glzhao/repos/config/_oh-my-zsh /home/glzhao/.oh-my-zsh

##############################################################################
# start
##############################################################################

USER root
CMD ["zsh"]
