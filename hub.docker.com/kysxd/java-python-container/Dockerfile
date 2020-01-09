FROM openjdk:8u181-jdk-slim-stretch

RUN apt-get update -y \
    && apt-get install -y \
    build-essential \
    checkinstall \
    apt-utils \
    && apt-get install -y \
    libreadline-gplv2-dev \
    libncursesw5-dev \
    libssl-dev \
    libsqlite3-dev \
    tk-dev \
    libgdbm-dev \
    libc6-dev \
    libbz2-dev \
    wget

RUN cd /usr/src \
    && wget https://www.python.org/ftp/python/3.5.6/Python-3.5.6.tgz \
    && tar xzf Python-3.5.6.tgz \
    && cd Python-3.5.6 \
    && ./configure --enable-optimizations \
    &&  make altinstall

RUN apt-get install -y \
    python3-dev \
    python3-pip \
    && pip3 install pipenv

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8
ENV TZ UTC

CMD ["bash"]
