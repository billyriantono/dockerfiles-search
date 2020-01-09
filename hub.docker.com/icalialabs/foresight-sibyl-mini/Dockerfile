# I: Development Stage: ========================================================
# In this stage we'll build the image used for development, including compilers,
# and development libraries. This is also a first step for building a releasable
# Docker image:

# 1: Use ruby 2.5.1 alpine 3.7 as base:
FROM ruby:2.5.1-alpine3.7 AS development

# 2: We'll set '/usr/src' path as the working directory:
WORKDIR /usr/src

# 3: We'll set the working dir as HOME and add the app's binaries path to $PATH:
ENV HOME=/usr/src PATH=/usr/src/bin:$PATH

# 4: Install the common runtime dependencies:
RUN apk add --no-cache less ca-certificates icu-libs nodejs yarn openssl tzdata

# 5: Install the development dependencies from alpine package manager:
RUN apk add --no-cache build-base cmake icu-dev

# 6: Copy just the Gemfile & Gemfile.lock, to avoid the build cache failing
# whenever any other file changed and installing dependencies all over again -
# a must if your'e developing this Dockerfile...
ADD Gemfile* /usr/src/

# 7: Install the current project gems - they can be safely changed later during
# development via `bundle install` or `bundle update`:
RUN bundle install --jobs=4 --retry=3

# 8: Set the default command:
CMD [ "rails", "server" ]

# II: Builder stage: ===========================================================
# In this stage we'll compile assets coming from the project's source, do some
# tests and cleanup. If the CI/CD that builds this image allows it, we should
# also run the app test suites here:

# 1: Use ruby 2.5.1 alpine 3.7 as base:
FROM ruby:2.5.1-alpine3.7 AS builder

# 2-7: We'll replicate the steps of "development" stage so we use as much cached
# layers as possible:
WORKDIR /usr/src
ENV HOME=/usr/src PATH=/usr/src/bin:$PATH
RUN apk add --no-cache less ca-certificates icu-libs nodejs yarn openssl tzdata
RUN apk add --no-cache build-base cmake icu-dev
ADD Gemfile* /usr/src/
RUN bundle install --jobs=4 --retry=3

# 8: Copy the rest of the application code
ADD . /usr/src

# 9: Precompile assets:
RUN export SECRET_KEY_BASE=10167c7f7654ed02b3557b05b88ece \
    RAILS_ENV=production && \
    rails assets:precompile && \
    rails secret > /dev/null

# 10: Remove installed gems that belong to the development & test groups - we'll
# copy the remaining system gems into the deployable image later:
RUN bundle config without development:test && bundle clean && rm -rf tmp/*

# III: Deployable stage: =======================================================
# In this stage, we build the final, deployable Docker image, which will be
# smaller than the images generated on previous stages:

# 1: Use ruby 2.5.1 (alpine 3.7) as base:
FROM ruby:2.5.1-alpine3.7 AS deployable

# 2-4: We'll replicate the steps from "development" & "builder" stage so we use
# the most cached layers as possible:
WORKDIR /usr/src
ENV HOME=/usr/src PATH=/usr/src/bin:$PATH
RUN apk add --no-cache less ca-certificates icu-libs nodejs yarn openssl tzdata

# 5: Set the '/code' and '/data' as VOLUMES (prevent changes in these from saving)
VOLUME ["/code", "/data"]

# 6: Copy the installed system gems from the BUILDER STAGE:
COPY --from=builder /usr/local/bundle /usr/local/bundle

# 7: Copy the app code from the BUILDER STAGE at the /usr/src directory:
COPY --from=builder /usr/src /usr/src

# 8: Set the RAILS/RACK_ENV and PORT default values:
ENV RAILS_ENV=production \
    RACK_ENV=production \
    PORT=3000 \
    RAILS_SERVE_STATIC_FILES=true \
    SECRET_KEY_BASE=0080596487c9bdf4358e75eie02c256fcc50a46b23e38ff27ecb985ff427

# 9: Check that there are no issues with rails' load paths, missing gems, etc:
RUN rails runner "puts 'Looks Good!'"

# 10: Add label-schema.org labels to identify the build info:
ARG SOURCE_BRANCH="master"
ARG SOURCE_COMMIT="000000"
ARG BUILD_DATE="2017-09-26T16:13:26Z"
ARG IMAGE_NAME="icalialabs/foresight-sibyl-mini:latest"

LABEL org.label-schema.build-date=$BUILD_DATE \
     org.label-schema.name="Icalia Foresight Sibyl Mini" \
     org.label-schema.description="Icalia Local Code Analysis Runner" \
     org.label-schema.vcs-url="https://github.com/IcaliaLabs/foresight.git" \
     org.label-schema.vcs-ref=$SOURCE_COMMIT \
     org.label-schema.schema-version="1.0.0-rc1"

RUN set -ex \
&& sed -i "s|icalialabs/foresight-sibyl-mini:development|$IMAGE_NAME|" config/application.rb \
&& sed -i "s|UNKNOWN_BUILD_DATE|$BUILD_DATE|" config/application.rb \
&& sed -i "s|UNKNOWN_COMMIT_SHA1|$SOURCE_COMMIT|" config/application.rb \
&& sed -i "s|UNKNOWN_COMMIT_BRANCH|$SOURCE_BRANCH|" config/application.rb

# 11: Generate the temporary directories in case they don't already exist:
RUN mkdir -p /usr/src/tmp/cache && \
mkdir -p /usr/src/tmp/pids && \
mkdir -p /usr/src/tmp/sockets

# 12: Set the default command - we set this last so we can cache the previous
# commands for other process types on Heroku:
CMD [ "puma" ]
