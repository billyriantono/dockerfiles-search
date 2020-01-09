# I: Development Stage: ========================================================
# In this stage we'll build the image used for development, including compilers,
# and development libraries. This is also a first step for building a releasable
# Docker image:

# 1: Use ruby 2.4.4 (alpine 3.7) as base:
FROM ruby:2.4.4-alpine3.7 AS development

# 2: We'll set the application path as the working directory
WORKDIR /usr/src/app

# 3: We'll set the working dir as HOME and add the app's binaries path to $PATH:
ENV HOME=/usr/src/app PATH=/usr/src/app/bin:$PATH

# 4: Install the runtime dependencies:
RUN apk add --no-cache ca-certificates less libpq openssl su-exec tzdata

# 5: Install the development dependency packages:
RUN apk add --no-cache build-base postgresql-dev

# 6: Copy the project's Gemfile + lock:
ADD Gemfile* /usr/src/app/

# 7: Install the current project gems - they can be safely changed later during
# development via `bundle install` or `bundle update`:
RUN bundle install --jobs=4 --retry=3

# 8: Set the default command:
CMD ["rails", "server", "-b", "0.0.0.0"]

# II: Builder stage: ===========================================================
# In this stage we'll compile assets coming from the project's source, do some
# tests and cleanup. If the CI/CD that builds this image allows it, we should
# also run the app test suites here:

# 1: Use ruby 2.4.4 (alpine 3.7) as base:
FROM ruby:2.4.4-alpine3.7 AS builder

# 2-7: We'll replicate the steps of "development" stage so we use as much cached
# layers as possible:
WORKDIR /usr/src/app
ENV HOME=/usr/src/app PATH=/usr/src/app/bin:$PATH
RUN apk add --no-cache ca-certificates less libpq openssl su-exec tzdata
RUN apk add --no-cache build-base postgresql-dev
ADD Gemfile* /usr/src/app/
RUN bundle install --jobs=4 --retry=3

# 8: Copy the rest of the application code
ADD . /usr/src/app

# 9: Remove installed gems that belong to the development & test groups - we'll
# copy the remaining system gems into the deployable image later:
RUN bundle config without development:test && bundle clean && rm -rf tmp/*

# III: Deployable stage: =======================================================
# In this stage, we build the final, deployable Docker image, which will be
# smaller than the images generated on previous stages:

# 1: Use ruby 2.4.4 (alpine 3.7) as base:
FROM ruby:2.4.4-alpine3.7 AS deployable

# 2-4: We'll replicate the steps from "development" & "builder" stage so we use
# the most cached layers as possible:
WORKDIR /usr/src/app
ENV HOME=/usr/src/app PATH=/usr/src/app/bin:$PATH
RUN apk add --no-cache ca-certificates less libpq openssl su-exec tzdata

# 5: Copy the installed system gems from the BUILDER STAGE:
COPY --from=builder /usr/local/bundle /usr/local/bundle

# 6: Copy the app code from the BUILDER STAGE at the /usr/src/app directory:
COPY --from=builder /usr/src/app /usr/src/app

# 7: Set the RAILS/RACK_ENV and PORT default values:
ENV RAILS_ENV=production RACK_ENV=production PORT=3000

# 8: Check that there are no issues with rails' load paths, missing gems, etc:
RUN export DATABASE_URL=postgres://postgres@example.com:5432/fakedb \
    AMQP_URL=amqp://guest:guest@amqp:5672 \
    SECRET_KEY_BASE=10167c7f7654ed02b3557b05b88ece && \
    rails runner "puts 'Looks Good!'"

# 9: Add image labelling:
ARG SOURCE_BRANCH
ARG SOURCE_COMMIT
ARG BUILD_DATE

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Icalia Foresight Vulcan" \
      org.label-schema.description="Tracks app development & it's associated cloud resources" \
      org.label-schema.vcs-url="https://github.com/IcaliaLabs/foresight.git" \
      org.label-schema.vcs-ref=$SOURCE_COMMIT \
      org.label-schema.schema-version="1.0.0-rc1"

RUN set -ex && \
 sed -i "s|UNKNOWN_BUILD_DATE|$BUILD_DATE|" app/controllers/info_controller.rb && \
 sed -i "s|UNKNOWN_COMMIT_SHA1|$SOURCE_COMMIT|" app/controllers/info_controller.rb && \
 sed -i "s|UNKNOWN_COMMIT_BRANCH|$SOURCE_BRANCH|" app/controllers/info_controller.rb

# 10: Generate the temporary directories in case they don't already exist:
RUN mkdir -p /usr/src/tmp/cache && \
   mkdir -p /usr/src/tmp/pids && \
   mkdir -p /usr/src/tmp/sockets && \
   chown -R nobody /usr/src/app

# 11: Set the container user to 'nobody':
USER nobody

# 12: Set the default command - we set this last so we can cache the previous
# commands for other process types on Heroku:
CMD [ "puma" ]
