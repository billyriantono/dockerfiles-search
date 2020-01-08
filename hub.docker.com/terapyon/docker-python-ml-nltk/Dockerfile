FROM terapyon/python-ml-base

RUN apt-get update -y
RUN apt-get install -y libmecab-dev
RUN apt-get install -y mecab mecab-ipadic-utf8

RUN pip install nltk
RUN pip install mecab-python3

#CMD ["/bin/bash"]
