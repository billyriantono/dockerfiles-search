
FROM manaysh/minimum

USER root

RUN apt-get update && \
    apt-get install -y default-jre default-jdk  && \
    apt-get install -y mecab libmecab-dev mecab-ipadic-utf8 swig && \
    apt-get install -y curl file && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN conda install -y libgcc

RUN git clone https://github.com/mana-ysh/conf.git

## Sudachi
RUN cp -r ${HOME}/conf/.sudachi ${HOME}/.sudachi && \
    sh ${HOME}/.sudachi/install.sh

## MeCab (neologd)
RUN cp -r ${HOME}/conf/.mecab ${HOME}/.mecab && \
    sh ${HOME}/.mecab/install_neologd.sh && \
    pip install mecab-python3

USER $NB_UID
