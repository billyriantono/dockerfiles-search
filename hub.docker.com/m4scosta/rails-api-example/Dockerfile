# Build stage
FROM ruby:2.6-alpine AS base

# Install system deps
RUN apk add --update --no-cache build-base postgresql-dev tzdata

WORKDIR /app

# Install gems
COPY Gemfile* /app/
RUN bundle config --global frozen 1 \
 && bundle install --without development test -j5 --retry 5 \
 && rm -rf /usr/local/bundle/cache/*.gem \
 && find /usr/local/bundle/gems/ -name "*.c" -delete \
 && find /usr/local/bundle/gems/ -name "*.o" -delete

ADD . /app


# Final stage
FROM ruby:2.6-alpine

# Labels
LABEL maintainer="costa.marcos.pro@gmail.com"

# Install system deps
RUN apk add --update --no-cache postgresql-dev tzdata

# Setup user
RUN addgroup -g 1000 -S app && adduser -u 1000 -S app -G app
USER app

# Copy app files and gems from base
COPY --from=base /usr/local/bundle/ /usr/local/bundle/
COPY --from=base --chown=app:app /app /app

# Env vars
ENV RAILS_ENV production

WORKDIR /app

EXPOSE 3000

CMD ["bundle", "exec", "rails", "server", "--binding", "0.0.0.0"]
