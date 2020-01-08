FROM tensorflow/tensorflow:1.11.0-py3
MAINTAINER BananaBb

# Update apt & install base
RUN apt-get update -y \
 && apt-get install -y \
    libicu-dev

# Install Package
RUN pip install -U gensim \
    spacy \
    textblob \
    scikit-learn
RUN pip install nltk \
    pyicu \
    polyglot==15.03.17 \
    hmmlearn \
    scipy \
    matplotlib \
    torch==1.0.1 -f https://download.pytorch.org/whl/cpu/stable \
    ftfy==4.4.3 \
    networkx \
    seaborn \
    pykg2vec==0.0.31 \
    pandas \
    Flask \
    statsmodels \
    xgboost \
    eli5 \
    snorkel-metal


EXPOSE 8888

CMD ["/bin/bash"]