FROM jupyter/datascience-notebook
MAINTAINER ottati <ottatiyarou@gmail.com>

# install some
USER root

# 日本語フォント
RUN apt-get update
RUN apt-get install -y ttf-kochi-gothic xfonts-intl-japanese xfonts-intl-japanese-big xfonts-kaname


# install mecab
RUN git clone https://github.com/taku910/mecab.git \
  && cd mecab/mecab \
  && ./configure  --enable-utf8-only \
  && make \
  && make check \
  && make install \
  && ldconfig \
  && cd ../mecab-ipadic \
  && ./configure --with-charset=utf8 \
  && make \
  && make install

# install neologd/mecab-ipadic-neologd
# no file command...
# RUN cd / \
#   && git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git \
#   && cd mecab-ipadic-neologd \
#   && ./bin/install-mecab-ipadic-neologd -n -y



USER jovyan

RUN pip install mecab-python3 python-levenshtein
