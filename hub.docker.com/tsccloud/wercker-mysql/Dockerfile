# werckerビルド環境: MySQL
FROM mysql:5.7
MAINTAINER Technosite Cloud
RUN apt-get -y update; \
    apt-get -y upgrade; \
    apt-get -y install \
        apt-utils \
        locales \
        locales-all; \
    apt-get clean; \
    apt-get autoclean; \
    apt-get autoremove; \
    sed -i -e "s/^# ja_JP/ja_JP/" /etc/locale.gen; \
    locale-gen; \
    update-locale LANG=ja_JP.UTF-8 LANGUAGE=ja_JP:ja; \
    cat /etc/mysql/my.cnf
ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
ENV LC_CTYPE ja_JP.UTF-8

# mysql
ADD charset.cnf /etc/mysql/conf.d/
ADD bind-address.cnf /etc/mysql/conf.d/
