FROM node:11.13.0-stretch
MAINTAINER Shanti Naik <visitsb@gmail.com>

# Defaults if not overridden by environment variables
ENV NODE_ENV production
ENV DEBUG multilevel2-http/server
ENV HOST 0.0.0.0
ENV PORT 80
ENV USER admin
ENV PASSWORD test
ENV DB /db

VOLUME ["${DB}"]
WORKDIR /home/node/app

RUN (/bin/rm -rf * && /bin/rm -rf .* && /bin/rm -rf *.*) || true \
 && /usr/bin/git clone --recurse-submodules --branch master https://github.com/visitsb/multilevel2-http.git . \
 && /usr/local/bin/npm upgrade \
  ; exit 0

# To use environment variables in CMD, you need to use shell.
# https://stackoverflow.com/a/52789442
# Override default CMD with our own
# https://github.com/nodejs/docker-node/blob/master/11/alpine/Dockerfile
CMD [ "/bin/sh", "-c", "/usr/local/bin/node /home/node/app/bin/multilevel2-http.js --host=${HOST} --port=${PORT} --user=${USER} --password=${PASSWORD} ${DB}" ]
