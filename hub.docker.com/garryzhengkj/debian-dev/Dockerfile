FROM debian:jessie

ADD .vimrc /root/.vimrc
ADD .ycm_extra_conf.py /root/.ycm_extra_conf.py

RUN apt-get update \
        && apt-get install -y --no-install-recommends \
                openssh-server \
                pwgen \
                gcc \
                g++ \
                gdb \
                libncurses5-dev \
                python \
                python-dev \
                python3 \
                python3-dev \
                ruby \
                ruby-dev \
                lua5.1  \
                lua5.1-dev \
                perl \
                libperl-dev \
                git \
                cmake \
                ctags \
                lrzsz \
                make \
                mlocate \
                xz-utils \
        && rm -r /var/lib/apt/lists/* \
        && mkdir -p /var/run/sshd \
        && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
        && sed -i "s/PermitRootLogin without-password/PermitRootLogin yes/g" /etc/ssh/sshd_config \
        && cd /tmp \
        && git clone https://github.com/vim/vim.git \
        && cd vim \
        && ./configure --with-features=huge \
                --enable-multibyte \
                --enable-rubyinterp=yes \
                --enable-pythoninterp=yes \
                --enable-python3interp=yes \
                --enable-perlinterp=yes \
                --enable-luainterp=yes \
                --enable-cscope \ 
                --prefix=/usr \
        && make -j4 \
        && make install \
        && update-alternatives --install /usr/bin/editor editor /usr/bin/vim 1 \
        && update-alternatives --set editor /usr/bin/vim \
        && update-alternatives --install /usr/bin/vi vi /usr/bin/vim 1 \
        && update-alternatives --set vi /usr/bin/vim \
        && git clone https://github.com/VundleVim/Vundle.vim.git /root/.vim/bundle/Vundle.vim \
        && vim -c PluginInstall -c q -c q \
        && cd /root/.vim/bundle/YouCompleteMe \
        && ./install.py --clang-completer \
        && sed -i 's/^colorscheme default/"colorscheme default/g' /root/.vimrc \
        && sed -i 's/^"colorscheme solarized/colorscheme solarized/g' /root/.vimrc \
        && rm -rf /tmp/*

ADD set_root_pw.sh /set_root_pw.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

ENV AUTHORIZED_KEYS **None**

EXPOSE 22
CMD ["/run.sh"]
