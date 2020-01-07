FROM ubuntu:15.04
MAINTAINER tobe tobeg3oogle@gmail.com

RUN apt-get update -y

RUN apt-get install -y git
RUN apt-get install -y emacs
RUN apt-get install -y vim

RUN apt-get install -y python-dev
RUN apt-get install -y python-pip
RUN apt-get install -y python-openssl
RUN apt-get install -y python-mysqldb
RUN apt-get install -y libmysqlclient-dev
RUN apt-get install -y python-mysql.connector

RUN pip install sphinx
RUN pip install tox
RUN pip install pbr
RUN pip install oslosphinx
RUN pip install rst2pdf
RUN pip install transifex-client
RUN pip install pylink
RUN pip install pika
RUN pip install netifaces
RUN pip install pyOpenSSL
RUN pip install jsonpatch
RUN pip install simplejson
RUN pip install jsonschema
RUN pip install paste
RUN pip install eventlet
RUN pip install pastescript
RUN pip install PasteDeploy
RUN pip install WebOb
Run pip install SQLALchemy

CMD /bin/bash
