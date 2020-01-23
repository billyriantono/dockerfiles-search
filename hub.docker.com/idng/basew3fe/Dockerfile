FROM idng/basenodejs

MAINTAINER IDNG <docker@idng.com>

RUN npm install -g connect express \
                   passport passport-local passport-twitter passport-facebook passport-linkedin \
                   forever \
                   elasticsearch cassandra-driver \
                   async q promise promises

# thrift
# geoip ip2location-nodejs ip2loc
#ip2loc is the unofficial module for ip2location

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/sbin/my_init"]
