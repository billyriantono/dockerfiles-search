FROM ruby
MAINTAINER dhcgn@mailbox.org

RUN apt-get update
RUN apt-get install -y node python-pygments

RUN gem install jekyll rdiscount kramdown jekyll-gist jemoji listen

VOLUME /src
EXPOSE 4000

WORKDIR /src
ENTRYPOINT ["jekyll"]