FROM alpine:latest
MAINTAINER Joaquín de la Zerda <joaquindelazerda@gmail.com>

# Install base and docl (gem)
RUN apk --update add curl ruby ruby-dev; \
       curl http://production.cf.rubygems.org/rubygems/rubygems-2.4.8.tgz > /tmp/rubygems-2.4.8.tgz; \
       tar xvzf /tmp/rubygems-2.4.8.tgz; \
       cd /tmp/rubygems-2.4.8; \
       ruby setup.rb; \
       gem install docl

CMD ["/bin/sh"]
