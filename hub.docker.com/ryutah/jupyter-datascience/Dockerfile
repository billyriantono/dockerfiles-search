FROM jupyter/datascience-notebook:c19283de5a6f

USER root

RUN apt-get update \
 && apt-get install -y mecab mecab-ipadic-utf8 libmecab-dev file

WORKDIR /tmp

RUN git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git \
 && ./mecab-ipadic-neologd/bin/install-mecab-ipadic-neologd -n -y -a \
 && rm -rf /tmp/mecab-ipadic-neologd

USER $NB_UID

ARG PYTHON_LIBS="mecab-python3 gensim"

RUN pip install $PYTHON_LIBS

WORKDIR /home/jovyan
