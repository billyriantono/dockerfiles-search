FROM ubuntu:16.04

RUN apt-get -y update \
    && apt-get -y upgrade \
    && apt-get install -y make\
    && apt-get install -y locales curl \
    && apt-get install -y xz-utils\
    && apt-get install -y file\
    && apt-get install -y sudo\
    && apt-get install -y wget\
    && apt-get install -y swig\
    && apt-get install -y lsof\
    && apt-get install -y build-essential software-properties-common git \
    && apt-get install apt-transport-https

RUN apt-get update -y \
    && : "python3 のセットアップ" \
    && apt-get install -y software-properties-common vim \
    && sudo add-apt-repository ppa:jonathonf/python-3.6 \
    && apt-get update \
    && apt-get install -y build-essential python3.6 python3.6-dev python3-pip python3.6-venv \
    && python3.6 -m pip install pip --upgrade \
    && mkdir /code \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8


RUN apt-get -y update \
    && : "オフライン インストール" \
    && apt-get install -y libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev \
    && apt-get -y update \
    && : "MeCabのインストール" \
    && apt-get -y install mecab libmecab-dev mecab-ipadic-utf8 \
    && git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git \
    && cd mecab-ipadic-neologd \
    && bin/install-mecab-ipadic-neologd -n -y \
    && apt-get update \
    && apt-get install -y software-properties-common vim \
    && apt-get update \
    && pip install mecab-python3

ENV LANG en_US.utf8
WORKDIR /code
ADD . /code/
ADD requirements.txt /code
RUN pip install -r requirements.txt

# ssh
ENV SSH_PASSWD "root:Docker!"
RUN apt-get update \
        && apt-get install -y --no-install-recommends dialog \
        && apt-get update \
	&& apt-get install -y --no-install-recommends openssh-server \
	&& echo "$SSH_PASSWD" | chpasswd

# COPY sshd_config /etc/ssh/
COPY init.sh /usr/local/bin/

RUN chmod u+x /usr/local/bin/init.sh
EXPOSE 8000 2222
ENTRYPOINT ["init.sh"]
