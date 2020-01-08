FROM cariandrum22/rails-base:2.2.0

MAINTAINER cariandrum22@gmail.com

# Prepare
RUN apt-get update

# Install mecab
RUN apt-get install -y --force-yes software-properties-common
RUN add-apt-repository -y universe
RUN add-apt-repository -y ppa:groonga/ppa
RUN apt-get update
RUN apt-get install -y --force-yes mecab mecab-ipadic libmecab-dev
RUN apt-get clean
