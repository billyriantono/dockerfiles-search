FROM bgolden/docker-pyenv:latest

RUN pyenv install 2.7.13
RUN pyenv install 3.4.6
RUN pyenv install 3.5.3
RUN pyenv install 3.6.0
RUN pyenv global 2.7.13 3.6.0 3.5.3 3.4.6

RUN pip3 install tox

ONBUILD COPY $BUILD_PATH /workspace

ONBUILD WORKDIR /workspace
ONBUILD CMD ["tox"]
