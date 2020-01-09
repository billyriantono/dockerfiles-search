FROM ruby:2.6

RUN apt-get update -qq
RUN apt-get install -y --no-install-recommends build-essential \
    zlib1g-dev libxslt-dev mysql-client sqlite3

RUN apt-get install -y python-pip

RUN pip install awsebcli --upgrade --user
RUN pip install awscli --upgrade --user

RUN echo PATH=~/.local/bin:$PATH >> ~/.bashrc 

RUN mkdir ~/.aws/ && touch ~/.aws/credentials && touch ~/.aws/config
