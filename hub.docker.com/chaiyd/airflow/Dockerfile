FROM python:3.7-alpine

###放置docker hub build，注释掉国内源
#RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
RUN apk add tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata \
    && apk add python-dev \
               gcc \
               g++ \
               linux-headers \
               libc-dev \
               libxml2 \
               libxml2-dev \
               libxslt \
               libxslt-dev \
               libstdc++ \
               libressl-dev \
               openssl-dev \
               mariadb \
               mysql \
               mysql-dev \
               git \
               swig \
               subversion \
               gfortran \
               freetds-dev \
               postgresql-dev

ARG app_path=/home/airflow
#ADD pip.conf /root/.pip/

RUN mkdir -p $app_path
RUN pip3 install virtualenv

ADD glibc-2.30-r0.tgz $app_path
RUN cd $app_path \
    && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
    && apk add ./glibc-2.30-r0.apk

RUN cd $app_path \
    mkdir venv3 \
    && python3 -m venv venv3/airflow \
    && source venv3/airflow/bin/activate \
    && pip install --upgrade pip \
    && pip install numpy \
    && pip install werkzeug \
    && pip install Flask \
    && pip install werkzeug \
    && pip install cython \
    && pip install pymssql \
    && pip install apache-airflow[mysql] \
    && pip install apache-airflow[hive] \
    && pip install apache-airflow[mssql] \
    && pip install apache-airflow[oracle] \
    && pip install apache-airflow[postgres]
        
ADD start.sh $app_path

WORKDIR $app_path

ENV AIRFLOW_HOME=/home/airflow

ENTRYPOINT ["/bin/sh","start.sh"]
