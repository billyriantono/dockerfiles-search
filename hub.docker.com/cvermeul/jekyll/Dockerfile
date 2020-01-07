FROM ruby

RUN apt-get update

RUN gem install jekyll

VOLUME /src
EXPOSE 4000

WORKDIR /src
ENTRYPOINT ["jekyll"]
