FROM centos:8

ENV PYTHON_VERSION 3.8.0

# yum
RUN set -x \
 && yum update -y \
 && yum groupinstall -y "development tools" \
 && yum install -y \
            bzip2-devel \
            gdbm-devel \
            libffi-devel \
            libuuid-devel \
            ncurses-devel \
            openssl-devel \
            readline-devel \
            sqlite-devel \
            tk-devel \
            wget \
            xz-devel \
            zlib-devel\
            sudo \
            git \
            unzip \
            curl \
 && rm -rf /var/cache/yum/* \
 && yum clean all

# Japanese Locale setting
#RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
#ENV LANG="ja_JP.UTF-8" \
#    LANGUAGE="ja_JP:ja" \
#    LC_ALL="ja_JP.UTF-8"

# Python install
ENV HOME /root
ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/bin:$PATH

RUN git clone https://github.com/yyuu/pyenv.git $HOME/.pyenv
RUN echo 'eval "$(pyenv init -)"' >> ~/.bashrc \
 && eval "$(pyenv init -)"

RUN pyenv install ${PYTHON_VERSION} \
 && pyenv global ${PYTHON_VERSION}

# pip update
RUN source ~/.bashrc && pip install --upgrade pip

# work directory
RUN mkdir /share
WORKDIR /share
