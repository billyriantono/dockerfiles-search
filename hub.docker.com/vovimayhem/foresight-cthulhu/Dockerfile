# I: Runtime Stage: ============================================================
# This is the stage where we build the runtime base image, which is used as the
# common ancestor by the rest of the stages, and contains the minimal runtime
# dependencies required for the application to run:

# 1: Use ruby 2.5.3 (alpine 3.8) as base:
FROM ruby:2.5.3-alpine3.8 AS runtime

# 2: We'll set '/usr/src' path as the working directory:
WORKDIR /usr/src

# 3: We'll set the working dir as HOME and add the app's binaries path to $PATH:
ENV HOME=/usr/src PATH=/usr/src/bin:$PATH

# 4: Install the common runtime dependencies using alpine's package manager:
RUN apk add --no-cache ca-certificates less libpq openssl tzdata

# II: Development Stage: =======================================================
# In this stage we'll build the image used for development, including compilers,
# and development libraries. This is also a previous step for building a
# releasable Docker image:

# 1: Start off from the runtime stage image:
FROM runtime AS development

# 2: Install the development dependencies using alpine's package manager:
RUN apk add --no-cache build-base postgresql-dev

# 3: Copy the app's Gemfile & Gemfile.lock. This prevents the build process miss
# the "bundle install" cached layer whenever the rest of the app code changes,
# and thus avoiding installing gems over and over again:
ADD Gemfile* /usr/src/

# 4: Install the current project gems - they can be safely changed later during
# development via `bundle install` or `bundle update`:
RUN bundle install --jobs=4 --retry=3

# 5: Set the default command:
CMD [ "rails", "server", "-b", "0.0.0.0" ]

# III: Builder stage: ===========================================================
# In this stage we'll compile assets coming from the project's source, do some
# tests and do some cleanup:

# 1: Start off from the development stage image:
FROM development AS builder

# 2: Copy the rest of the application code
ADD . /usr/src

# 3: Remove installed gems that belong to the development & test groups:
RUN bundle config without development:test \
 && bundle clean \
 && rm -rf tmp/* \
 # Remove unneeded files (cached *.gem, *.o, *.c)
 && rm -rf /usr/local/bundle/cache/*.gem \
 && find /usr/local/bundle/gems/ -name "*.c" -delete \
 && find /usr/local/bundle/gems/ -name "*.o" -delete

# IV: Deployable stage: ========================================================
# In this stage, we build the final, deployable Docker image, which will be
# smaller than the images generated on previous stages:

# 1: Start off from the runtime stage image:
FROM runtime AS deployable

# 2: Copy the installed system gems from the BUILDER STAGE:
COPY --from=builder /usr/local/bundle /usr/local/bundle

# 3: Set 'nobody' as the owner of the '/usr/src' path:
RUN chown -R nobody:nobody /usr/src

# 4: Set the container user to 'nobody':
USER nobody

# 5: Copy the app code from the BUILDER STAGE at the /usr/src directory:
COPY --from=builder --chown=nobody:nobody /usr/src /usr/src

# 6: Generate the temporary directories in case they don't already exist:
RUN mkdir -p /usr/src/tmp/cache \
 && mkdir -p /usr/src/tmp/pids \
 && mkdir -p /usr/src/tmp/sockets

# 7: Set the RAILS/RACK_ENV and PORT default values:
ENV RAILS_ENV=production RACK_ENV=production PORT=3000 RAILS_LOG_TO_STDOUT=true

# 8: Check that there are no issues with rails' load paths, missing gems, etc:
RUN export DATABASE_URL=postgres://postgres@example.com:5432/fakedb \
    AMQP_URL=amqp://guest:guest@amqp:5672 \
    SECRET_KEY_BASE=10167c7f7654ed02b3557b05b88ece && \
    rails runner "puts 'Looks Good!'"

# 9: Add label-schema.org labels to identify the build info:
ARG SOURCE_BRANCH="master"
ARG SOURCE_COMMIT="000000"
ARG BUILD_DATE="2017-09-26T16:13:26Z"
ARG IMAGE_NAME="icalialabs/foresight-cthulhu:latest"

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Icalia Foresight Cthulhu" \
      org.label-schema.description="Icalia Foresight integration with Github" \
      org.label-schema.vcs-url="https://github.com/IcaliaLabs/foresight.git" \
      org.label-schema.vcs-ref=$SOURCE_COMMIT \
      org.label-schema.schema-version="1.0.0-rc1"

RUN sed -i "s|icalialabs/foresight-cthulhu:development|$IMAGE_NAME|" config/application.rb \
 && sed -i "s|UNKNOWN_BUILD_DATE|$BUILD_DATE|" config/application.rb \
 && sed -i "s|UNKNOWN_COMMIT_SHA1|$SOURCE_COMMIT|" config/application.rb \
 && sed -i "s|UNKNOWN_COMMIT_BRANCH|$SOURCE_BRANCH|" config/application.rb

# 10: Set the default command:
CMD [ "puma" ]
