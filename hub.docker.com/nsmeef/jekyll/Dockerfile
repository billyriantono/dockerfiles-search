FROM debian:jessie

MAINTAINER Nathan Smith <nathn.smith@googlemail.com>

RUN apt-get update && \
    apt-get install -y ruby make gcc ruby-dev && \
    gem update --system && \
    gem install jekyll jekyll-sitemap jekyll-feed 

WORKDIR /home/blog

CMD jekyll serve --host 0.0.0.0 --port 80 --incremental
