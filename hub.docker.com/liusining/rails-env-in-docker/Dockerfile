FROM ruby:2.4.3
RUN apt-get update -y \
    && apt-get install -y \
        libmysqlclient-dev \
        --fix-missing --no-install-recommends\
    && apt-get -q clean \
    && rm -rf /var/lib/apt/lists

ENV TZ=Asia/Chongqing
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN gem install bundler

