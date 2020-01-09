FROM debian:jessie
ENV HOME=/root PYENV_ROOT=/opt/pyenv PATH=/opt/pyenv/shims:/opt/pyenv/bin:$PATH DEBIAN_FRONTEND=noninteractive

# remove several traces of debian python
RUN sed -i -e 's/httpredir.debian.org/mirror.yandex.ru/g' /etc/apt/sources.list \
    && apt-get update -q \
    && apt-get upgrade -q -y \
    && apt-get install -y \
        # list of pyenv requirements https://github.com/yyuu/pyenv/wiki/Common-build-problems#requirements
        build-essential \
        curl \
        git \
        libbz2-dev \
        libncurses5-dev \
        libreadline-dev \
        libsqlite3-dev \
        libssl-dev \
        zlib1g-dev \

    # cleanup
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm /var/log/alternatives.log /var/log/apt/history.log /var/log/apt/term.log /var/log/dpkg.log \

    # pyenv part
    && curl https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash \
    && pyenv update \
    && pyenv install 2.7.11 \
    && pyenv install  3.5.1 \
    && pyenv global 3.5.1 2.7.11 \
    && pip install tox

CMD ["tox"]