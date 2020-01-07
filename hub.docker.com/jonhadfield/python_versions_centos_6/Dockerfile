FROM centos:6

RUN yum groupinstall -y "Development tools" && \
    yum install -y libyaml-devel git zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel && \
    curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash && \
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile && \
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile && \
    echo 'eval "$(pyenv init -)"' >> ~/.profile && \
    echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.profile && \
    . ~/.profile && \
    pyenv install 2.6.9 && \
    pyenv install 2.7.12 && \
    pyenv install 3.5.2 && \
    pyenv global 3.5.2 && \
    pip install pip tox -U

ENV HOME  /root
ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH
