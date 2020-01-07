# Visual Studio Code + Python

FROM tegieng7/vscode

RUN apt-get update && apt-get -y install \
    --no-install-recommends \
    python \
    python-pip \
    exuberant-ctags \
    python-dev \
    gcc \
 && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip
RUN pip install setuptools virtualenv
RUN pip install pylint pep8 autopep8 pydocstyle rope

RUN ${VSCODE} --install-extension ms-python.python
RUN ${VSCODE} --install-extension njpwerner.autodocstring
RUN ${VSCODE} --install-extension PKief.material-icon-theme

ADD utils/settings.json /code/config/User
RUN chown -R ${USERNAME}:${USERNAME} /code


