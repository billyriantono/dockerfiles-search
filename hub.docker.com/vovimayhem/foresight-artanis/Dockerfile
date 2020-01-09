# Stage I: Runtime =============================================================
# Step 1: Start off from the ruby official image, alpine version:
FROM ruby:2.5.3-alpine AS runtime

# Step 2: Set the home to the code path, and add the code executables to $PATH:
ENV HOME=/usr/src PATH=/usr/src/bin:$PATH

# Step 3: Set the main working directory:
WORKDIR /usr/src

# Step 4: Add the runtime packages (needed for the app to run) using Alpine's
# package manager:
RUN apk add --no-cache ca-certificates less libpq nodejs openssl tzdata

# Stage II: Development ========================================================
# Step 5: Use the "runtime" stage as the starting point:
FROM runtime AS development

# Step 6: Add the development packages (compilers, dev headers, etc):
RUN apk add --no-cache \
  build-base \
  chromium \
  chromium-chromedriver \
  git \
  postgresql-dev \
  yarn

# Step 7: Copy the project's Gemfile:
COPY Gemfile* /usr/src/

# Step 8: Download & Install the project's ruby libraries:
RUN bundle install --jobs=4 --retry=3

# Step 9: Set the default command for development images:
CMD ["rails", "server", "-b", "0.0.0.0", "-p", "3000"]

# Stage III: Builder ===========================================================
# Step 10: Pick off from development image:
FROM development AS builder

# Step 11: Copy the rest of the code:
COPY . /usr/src

# Step 12: Precompile assets:
RUN export DATABASE_URL=postgres://postgres@example.com:5432/fakedb \
    AMQP_URL=amqp://guest:guest@amqp:5672 \
    SECRET_KEY_BASE=10167c7f7654ed02b3557b05b88ece \
    RAILS_ENV=production && \
    rails assets:precompile && \
    rails secret > /dev/null

# Step 13: Remove installed gems that belong to the development & test groups -
# we'll copy the remaining system gems into the deployable image later:
RUN bundle config without development:test && bundle clean && rm -rf tmp/*

# Stage 4: Release =============================================================
# Step 14: Use the runtime stage as our image base:
FROM runtime AS release

# Step 15: Copy the installed system gems from the builder stage:
COPY --from=builder /usr/local/bundle /usr/local/bundle

# Step 16: Copy the application code from the builder stage at the /usr/src
# directory, along with the precompiled assets, setting the owner to 'nobody':
COPY --from=builder --chown=nobody:nobody /usr/src /usr/src

# Step 17: Set the container user to 'nobody', so it always run unprivileged:
USER nobody

# Step 18: Set the RAILS/RACK_ENV and PORT default values:
ENV RAILS_ENV=production RACK_ENV=production PORT=3000

# Step 19: Generate the temporary directories in case they don't already exist:
RUN mkdir -p /usr/src/tmp/cache /usr/src/tmp/pids /usr/src/tmp/sockets

# Step 20: Check that there are no issues with rails' load paths, missing gems,
# etc:
RUN export DATABASE_URL=postgres://postgres@example.com:5432/fakedb \
    AMQP_URL=amqp://guest:guest@amqp:5672 \
    SECRET_KEY_BASE=10167c7f7654ed02b3557b05b88ece && \
    rails runner "puts 'Looks Good!'"

# Step 21: Set the container's default command:
CMD [ "puma" ]

# Step 22 thru 26: Add label-schema.org labels to identify the build info:
ARG SOURCE_BRANCH="master"
ARG SOURCE_COMMIT="000000"
ARG BUILD_DATE="2017-09-26T16:13:26Z"
ARG IMAGE_NAME="vovimayhem/foresight-artanis:latest"

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Icalia Foresight Artanis" \
      org.label-schema.description="Identity services provider for Icalia apps" \
      org.label-schema.vcs-url="https://github.com/IcaliaLabs/foresight.git" \
      org.label-schema.vcs-ref=$SOURCE_COMMIT \
      org.label-schema.schema-version="1.0.0-rc1"

# Step 27: Modify the app code with the label-schema.org labels to identify
# the build info through the API:
RUN set -ex \
 && sed -i "s|vovimayhem/foresight-artanis:development|$IMAGE_NAME|" config/application.rb \
 && sed -i "s|UNKNOWN_BUILD_DATE|$BUILD_DATE|" config/application.rb \
 && sed -i "s|UNKNOWN_COMMIT_SHA1|$SOURCE_COMMIT|" config/application.rb \
 && sed -i "s|UNKNOWN_COMMIT_BRANCH|$SOURCE_BRANCH|" config/application.rb
