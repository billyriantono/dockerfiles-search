FROM ubuntu


MAINTAINER liuping <liuping@fireliuping.me>


RUN apt update && apt install -y build-essential ruby rubygems ruby-dev

RUN gem install jekyll

RUN mkdir /data

VOLUME ["/data"]

EXPOSE 4000

WORKDIR /data

CMD ["git", "clone", "https://github.com/8de4732a/8de4732a.github.io.git"]

