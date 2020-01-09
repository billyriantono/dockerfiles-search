FROM unicell/dind-go:1.3
MAINTAINER Qiu Yu <unicell@gmail.com>

RUN apt-get update -qqy
RUN apt-get install -y python-dev python-pip python-virtualenv
RUN apt-get install -y libffi-dev libxml2-dev libxslt1-dev libmysqlclient-dev libpq-dev
RUN pip install MySQL-python
RUN pip install python-keystoneclient python-novaclient python-glanceclient python-neutronclient python-swiftclient
