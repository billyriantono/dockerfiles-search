FROM phusion/passenger-nodejs:0.9.18

MAINTAINER Nick Breen <nick@foobar.net.nz>

RUN npm install -g loadtest

ENTRYPOINT ["/sbin/my_init", "--"]
CMD ["loadtest"]
