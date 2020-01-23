### Dockerfile --- spacemacs-docker dockerfile with Emacs25.x
##
## Copyright (c) 2012-2017 Sylvain Benner & Contributors
##
## Author: Eugene "JAremko" Yaremenko <w3techplayground@gmail.com>
##
##
## This file is not part of GNU Emacs.
##
### License: GPLv3
##
## See spacemacs/layers/+distributions/spacemacs-docker/README.org

FROM et2010/docker-emacs:latest
# FROM jare/emacs:emacs24
# Emacs snapshot
# FROM jare/emacs:testing

MAINTAINER et2010 <jianwang.academic@gmail.com>

ENV UNAME="spacemacser" \
    UID="1000"

# Default fonts
COPY ./fonts/* /tmp/
ENV NNG="NanumGothic-Regular.ttf" \
    SCP="1.050R-it.tar.gz"
RUN mkdir -p /usr/local/share/fonts \
    && cd /tmp && tar -xzf "${SCP}" -C /usr/local/share/fonts \
    && cp "${NNG}" /usr/local/share/fonts \
    && fc-cache -fv \
    && rm -rf /tmp/* /var/lib/apt/lists/* /root/.cache/*

# UHOME is /home/emacs (from jare/emacs)
COPY . ${UHOME}/.emacs.d

# Init Spacemacs
RUN cp ${UHOME}/.emacs.d/core/templates/.spacemacs.template ${UHOME}/ \
    && mv ${UHOME}/.spacemacs.template ${UHOME}/.spacemacs \
    && sed -i "s/\(-distribution 'spacemacs\)/\1-docker/" \
    ${UHOME}/.spacemacs \
    && asEnvUser emacs -batch -u ${UNAME} -kill \
    && asEnvUser emacs -batch -u ${UNAME} -kill \
    && chmod ug+rw -R ${UHOME}

# Test Spacemacs
RUN asEnvUser make -C ${UHOME}/.emacs.d/tests/core/ test \
    && cd ${UHOME}/.emacs.d \
    && printf "SPACEMACS REVISION: %s\n" "$(git rev-parse --verify HEAD)"

# Install pyenv
ENV PYVERS='3.6.2'
RUN apt-get update && \
    # This is basically the list from
    # https://github.com/yyuu/pyenv/wiki/Common-build-problems
    apt-get install build-essential libssl-dev zlib1g-dev libbz2-dev \
        libreadline-dev libsqlite3-dev llvm libncurses5-dev \
        libncursesw5-dev xz-utils && \

    # Install pyenv and pyenv-virtualenv
    git clone https://github.com/yyuu/pyenv.git ${UHOME}/.pyenv && \
    git clone https://github.com/yyuu/pyenv-virtualenv.git \
        ${UHOME}/.pyenv/plugins/pyenv-virtualenv && \

    # Build python with pyenv
    ${UHOME}/.pyenv/plugins/python-build/bin/python-build \
        -v ${PYVERS} ${UHOME}/.pyenv/versions/${PYVERS} && \

    # Create a file of the pyenv init commands
    echo 'export PYENV_ROOT="$UHOME/.pyenv"' >> pyenvinit && \
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> pyenvinit && \
    echo 'eval "$(pyenv init -)"' >> pyenvinit && \
    echo 'eval "$(pyenv virtualenv-init -)"' >> pyenvinit && \

    # Configure bash and zsh (in case it is installed later) for pyenv
    cat pyenvinit >> ${UHOME}/.bashrc && \
    cat pyenvinit >> ${UHOME}/.zshenv && \
    rm pyenvinit && \

    # Set the user's global version to the python we just built
    echo "$PYVERS" > ${UHOME}/.pyenv/version && \

    # Correct the owner and group of all the files root created for the user
    chown -R ${UNAME} ${UHOME} && \
    chgrp -R ${GNAME} ${UHOME} && \
    chmod ug+rw -R ${UHOME} && \

    # Remove build tools to save a bunch of space
    apt-get autoremove build-essential llvm && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /root/.cache/*

# Setup virtualenv
SHELL ["asEnvUser", "/bin/bash", "-c"]
ENV VENV_NAME="venv"
RUN source ${UHOME}/.bashrc \
    && pyenv virtualenv ${VENV_NAME} \
    && echo 'source ${UHOME}/.pyenv/versions/${VENV_NAME}/bin/activate' >> ${UHOME}/.bashrc

# Install apt-select
RUN source ${UHOME}/.bashrc \
    && pip install apt-select \
    && rm -rf ${UHOME}/.cache/pip/*

# Find out the fastest apt mirror
RUN source ${UHOME}/.bashrc \
    && cd ${UHOME} \
    && apt-select \
    && sudo mv -f sources.list /etc/apt/

SHELL ["/bin/sh", "-c"]
RUN ln -s \
    ${UHOME}/.emacs.d/layers/+distributions/spacemacs-docker/deps-install/run \
    /usr/local/sbin/install-deps \
    && chown root:root /usr/local/sbin/install-deps \
    && chmod 770 /usr/local/sbin/install-deps

# Install global dependencies (if any exists)
RUN install-deps

# Entrypoint and deps installation script will recreate it.
RUN userdel $UNAME \
    && groupdel $GNAME
