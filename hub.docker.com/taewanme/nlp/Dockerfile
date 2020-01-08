FROM ubuntu:18.04
MAINTAINER Taewan Kim <taewanme@gmail.com>

USER root


RUN apt-get update \
   &&  apt-get install -y curl apt-utils git make build-essential \
               libssl-dev libffi-dev zlib1g-dev libbz2-dev libreadline-dev   \
               libsqlite3-dev python3.6 python-pip python3-pip libjpeg8-dev python-dev \
               language-pack-ko python3-dev libxml2 libxml2-dev libxslt1-dev \
               fonts-nanum fonts-nanum-coding fonts-nanum-extra \
               cmake git wget unzip yasm pkg-config libswscale-dev \
               libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libavformat-dev libpq-dev \
   && apt-get clean \
   && rm -rf /var/lib/apt/lists/*


# set locale ko_KR
RUN locale-gen ko_KR.UTF-8
ENV LANG ko_KR.UTF-8
ENV LANGUAGE ko_KR.UTF-8
ENV LC_ALL ko_KR.UTF-8

RUN python3 -m pip install --upgrade pip

RUN pip3 install numpy          \
 && pip3 install Pandas         \
 && pip3 install Theano         \
 && pip3 install NLTK           \
 && pip3 install gensim          \
 && pip3 install beautifulsoup4       \
 && pip3 install jupyter         \
 && pip3 install feedparser  \
 && pip3 install PyPDF2      \
 && pip3 install keras      \
 && pip3 install python-docx \
 && pip3 install scikit-learn  \
 && pip3 install mglearn

RUN [ "python3", "-c", "import nltk; nltk.download('all')" ]


RUN mkdir -p /root/.jupyter/
COPY jupyter_notebook_config.py /root/.jupyter/
COPY start-notebook.sh /usr/local/bin

EXPOSE 8888

VOLUME ["/root/ipython"]
WORKDIR /root

ENTRYPOINT ["/bin/bash", "start-notebook.sh"]
