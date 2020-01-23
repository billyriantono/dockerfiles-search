FROM ubuntu:16.04
MAINTAINER andyzhshg <andyzhshg@gmail.com>

RUN apt-get update
RUN apt-get install -y git vim curl

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

RUN npm install hexo-cli -g

COPY build_blog.sh /build_blog.sh

CMD ["/build_blog.sh"]
