# Dev for Spark Docs
FROM ubuntu:16.04
MAINTAINER Shixiong Zhu <zsxwing@gmail.com>

RUN apt-get update && apt-get -y install gcc make ruby ruby-dev python-pip openjdk-8-jdk
RUN gem install jekyll
RUN gem install jekyll-redirect-from
RUN pip install Pygments
RUN pip install sphinx
RUN gem install pygments.rb

EXPOSE 4000

ADD start.sh /root/

CMD /root/start.sh
