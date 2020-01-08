FROM alpine:latest

ENV NODE_PATH /install/node_modules/
ENV PATH /install/node_modules/.bin:$PATH

RUN apk --update add autoconf automake libtool nasm build-base git nodejs python ruby ruby-dev nodejs-dev npm zlib-dev && \
  npm i npm@latest -g && \
  rm -rf /var/cache/apk/* && \
  npm install -g grunt-cli && \
  gem install listen sass compass scss_lint --no-document