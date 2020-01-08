FROM node:10.14.2-alpine

ENV NODE_ENV development
ENV RAILS_ENV development


# Additional Rails application dependencies
RUN apk add --no-cache --update build-base \
    ruby \
    linux-headers \
    git \
    postgresql-dev \
    tzdata