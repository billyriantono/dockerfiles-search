FROM centos:centos7

ADD .vimrc /root/.vimrc
ADD .ycm_extra_conf.py /root/.ycm_extra_conf.py

RUN rpm --rebuilddb \
    && rpm --import \
        http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7 \
    && rpm --import \
        https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7 \
    && yum -y install \
            --setopt=tsflags=nodocs \
            --disableplugin=fastestmirror \
        epel-release \
        openssh-server \
        pwgen \
        gcc \
        gcc-c++ \
        gdb \
        ncurses-devel \
        python \
        python-devel \
        python3 \
        python3-devel \
        ruby \
        ruby-devel \
        lua \
        lua-devel \
        perl \
        perl-devel \
        git \
        cmake \
        ctags \
        lrzsz \
        make \
        mlocate \
        xz \
        luajit \
        luajit-devel \
        tcl \
        tcl-devel \
        perl-ExtUtils-ParseXS \
        perl-ExtUtils-XSpp \
        perl-ExtUtils-CBuilder \
        perl-ExtUtils-Embed \
        readline \
        readline-devel \
    && yum -y remove vim-minimal \
    && rm -f /etc/ssh/ssh_host_ecdsa_key /etc/ssh/ssh_host_rsa_key \
    && ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_ecdsa_key \
    && ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key \
    && sed -i "s/#UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
    && cd /tmp \
    && git clone https://github.com/vim/vim.git \
    && cd vim \
    && ./configure \ 
        --with-features=huge \
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
    && yum clean all \
    && rm -rf /etc/ld.so.cache \
    && rm -rf /sbin/sln \
    && rm -rf /usr/{{lib,share}/locale,share/i18n,{lib,lib64}/gconv,bin/localedef,sbin/build-locale-archive} \
    && rm -rf /{root,tmp,var/cache/{ldconfig,yum}}/*

ADD set_root_pw.sh /set_root_pw.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

ENV AUTHORIZED_KEYS **None**

EXPOSE 22
CMD ["/run.sh"]
