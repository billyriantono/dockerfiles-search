FROM ruby:2.6.0-alpine3.8
ENV APP_DATA_DIR /usr/share/app-data
ENV APP_DIR /usr/share/app
RUN mkdir -p ${APP_DATA_DIR}
RUN gem install mustache 
WORKDIR /usr/share/app/

COPY ./app /usr/share/app/

# For debugging
RUN apk add --no-cache ruby-dev build-base ruby-irb emacs-nox git
RUN gem install byebug
