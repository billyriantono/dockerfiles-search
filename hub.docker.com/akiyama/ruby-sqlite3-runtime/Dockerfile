FROM akiyama/ruby
MAINTAINER Ryosuke Akiyama <ryosuke.akiyama@broadleaf.co.jp>

RUN apt-get install --no-install-recommends -y -q libsqlite3-dev

WORKDIR /app
ONBUILD ADD Gemfile /app/Gemfile
ONBUILD ADD Gemfile.lock /app/Gemfile.lock
ONBUILD RUN ["/usr/bin/bundle", "install", "--without=development", "test", "--deployment"]
ONBUILD ADD . /app

EXPOSE 8080
CMD []
ENV APPSERVER webrick
ENTRYPOINT /usr/bin/bundle exec rackup -p 8080 /app/config.ru -s $APPSERVER
