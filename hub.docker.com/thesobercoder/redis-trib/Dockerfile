FROM ruby:2.4-alpine3.6
LABEL maintainer="Soham Dasgupta <soham1.dasgupta@gmail.com>"
RUN gem install redis
WORKDIR /usr/local/bin
ADD redis-trib.rb /usr/local/bin/redis-trib.rb
RUN chmod 755 /usr/local/bin/redis-trib.rb
ENTRYPOINT ["/usr/local/bin/redis-trib.rb"]
