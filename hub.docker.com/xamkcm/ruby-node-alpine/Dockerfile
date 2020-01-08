# System setup
FROM library/alpine:latest
MAINTAINER Max McKenzie hello@maxmckenzie.uk
RUN apk update && apk upgrade
# install much ruby silliness
RUN apk add --update ruby ruby-dev ruby-irb ruby-rake ruby-io-console ruby-bigdecimal ruby-json ruby-bundler
RUN apk add --update ruby-dev build-base libxml2-dev libxslt-dev pcre-dev libffi-dev mariadb-dev postgresql-dev
RUN apk add --update git libstdc++ tzdata bash ca-certificates
# turn off no documentation warning
RUN echo 'gem: --no-document' > /etc/gemrc
RUN ruby -v
# install node
RUN apk add --update python nodejs-current-npm
RUN node -v
# install gem and node deps
RUN gem install sass compass font-awesome-sass
RUN gem install --pre sass-css-importer
RUN gem install breakpoint -v 2.7.1
RUN gem install modular-scale -v 2.1.1
RUN npm install -g grunt-cli