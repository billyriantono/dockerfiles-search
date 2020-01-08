FROM rocker/tidyverse:3.6.1

# Change environment to Japanese(Character and DateTime)
RUN apt-get -y update \
  && apt-get -y install task-japanese \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
RUN sed -i '$d' /etc/locale.gen \
  && echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen \
  && locale-gen ja_JP.UTF-8 \
  && /usr/sbin/update-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
RUN /bin/bash -c "source /etc/default/locale"
RUN ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN install2.r --error --deps TRUE odbc

# install odbc driver
RUN apt-get -y update \
  && apt-get -y install unixodbc unixodbc-dev --install-suggests \
  && apt-get -y install odbc-postgresql \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
