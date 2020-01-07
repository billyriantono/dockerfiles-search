FROM docker.elastic.co/elasticsearch/elasticsearch:7.4.1

LABEL MAINTAINER=ucsdets

# python2-pip
RUN yum update -y
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python get-pip.py

# nodejs
RUN curl -sL https://rpm.nodesource.com/setup_10.x | bash -
RUN yum install nodejs -y

# install tools
RUN pip install -U elasticsearch-curator
RUN npm install elasticdump -g