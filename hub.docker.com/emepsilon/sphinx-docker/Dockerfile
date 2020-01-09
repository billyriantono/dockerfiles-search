FROM python:3

MAINTAINER EmEpsilon

RUN apt update
RUN apt install sudo -y
RUN apt install mecab mecab-ipadic-utf8 libmecab-dev swig -y
RUN pip install sphinx recommonmark sphinx_rtd_theme sphinx-tsegsearch mecab-python3
RUN apt install git -y
RUN git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git
RUN mv mecab-ipadic-neologd /tmp
RUN /tmp/mecab-ipadic-neologd/bin/install-mecab-ipadic-neologd -n -a -y
