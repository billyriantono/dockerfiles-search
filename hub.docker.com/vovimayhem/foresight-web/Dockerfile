# I: Development Stage: ========================================================
# In this stage we'll build the image used for development, including compilers,
# and development libraries. This is also a first step for building a releasable
# Docker image:

# 1: Use node 6 as base:
FROM node:6-alpine as development

# 2: We'll set the application path as the working directory
WORKDIR /usr/src

# 3: We'll add the app's binaries path to $PATH and set the $HOME to the app folder:
ENV HOME=/usr/src PATH=/usr/src/bin:$PATH

# 4: Install runtime dependencies (jq & pup)
RUN apk add --no-cache ca-certificates jq openssl \
 && export PUP_VERSION=0.4.0 \
 && export PUP_SHA256=ec3d29e9fb375b87ac492c8b546ad6be84b0c0b49dab7ff4c6b582eac71ba01c \
 && wget -O pup.zip "https://github.com/ericchiang/pup/releases/download/v${PUP_VERSION}/pup_v${PUP_VERSION}_linux_amd64.zip" \
 && echo "$PUP_SHA256 *pup.zip" | sha256sum -c - \
 && unzip pup.zip -d /usr/bin

# 5: Install build & test dependencies:
# - git (required by bower), ember-cli, bower & yarn and friends
RUN apk add --no-cache chromium git \
 && npm install -g ember-cli bower yarn check-dependencies

# 6: Build strictly-development dependencies (watchman):
RUN apk add --no-cache autoconf automake build-base curl linux-headers python-dev \
 && export WATCHMAN_VERSION=4.7.0 \
 && curl -SL "https://github.com/facebook/watchman/archive/v${WATCHMAN_VERSION}.tar.gz" | tar -xz -C /tmp/ \
 && cd /tmp/watchman-${WATCHMAN_VERSION} \
 && ./autogen.sh \
 && ./configure \
 && make \
 && make install

# 7: Set the default command:
CMD ["ember", "server", "--live-reload-port", "35730"]

# II: Builder stage: ===========================================================
# In this stage we'll compile assets coming from the project's source, do some
# tests and cleanup. If the CI/CD that builds this image allows it, we should
# also run the app test suites here:

# 1: Use node 6 as base:
FROM node:6-alpine as builder

# 2-5: We'll replicate the steps of "development" stage so we use as much cached
# layers as possible:
WORKDIR /usr/src
ENV HOME=/usr/src PATH=/usr/src/bin:$PATH
RUN apk add --no-cache ca-certificates jq openssl \
 && export PUP_VERSION=0.4.0 \
 && export PUP_SHA256=ec3d29e9fb375b87ac492c8b546ad6be84b0c0b49dab7ff4c6b582eac71ba01c \
 && wget -O pup.zip "https://github.com/ericchiang/pup/releases/download/v${PUP_VERSION}/pup_v${PUP_VERSION}_linux_amd64.zip" \
 && echo "$PUP_SHA256 *pup.zip" | sha256sum -c - \
 && unzip pup.zip -d /usr/bin
RUN apk add --no-cache chromium git \
 && npm install -g ember-cli bower yarn check-dependencies

# 6: Set the desired api endpoints:
ENV ARTANIS_URL=https://artanis.icalialabs.com \
    VULCAN_URL=https://vulcan.icalialabs.com \
    SIBYL_URL=https://sibyl.icalialabs.com \
    CTHULHU_URL=https://cthulhu.icalialabs.com

# 7: We'll copy just the package.json + yarn.lock files and bower stuff, so we
# can ignore changes on the rest of the code and cache the app dependencies:
ADD package.json yarn.lock bower.json /usr/src/

# 8: Install the app npm dependencies within the Docker build context:
RUN set -ex && yarn install && bower install --allow-root

# 9: We'll copy the rest of the app source code:
ADD . /usr/src/

# 10: Run tests (or not):
# RUN ember test

# 11: Build the app:
RUN ember build --environment="production"

# III: Deployable stage: =======================================================
# In this stage, we build the final, deployable Docker image, which will be
# smaller than the images generated on previous stages:

# 1: Start off from IcaliaLabs' mini-nginx image:
FROM icalialabs/mini-nginx:latest AS deployable

# 2: Install jq (see https://stedolan.github.io/jq/) and pup (see
# https://github.com/ericchiang/pup), which enable the entrypoint to update the
# app's config meta tag with the current environment variable's values:
RUN apk add --no-cache ca-certificates jq openssl \
  && cd /tmp \
  && export PUP_VERSION=0.4.0 \
  && export PUP_SHA256=ec3d29e9fb375b87ac492c8b546ad6be84b0c0b49dab7ff4c6b582eac71ba01c \
  && wget -O pup.zip "https://github.com/ericchiang/pup/releases/download/v${PUP_VERSION}/pup_v${PUP_VERSION}_linux_amd64.zip" \
  && echo "$PUP_SHA256 *pup.zip" | sha256sum -c - \
  && unzip pup.zip -d /usr/bin \
  && cd $HOME \
  && rm -rf /tmp/*

# 3: Copy the compiled ember app (which was compiled in the previous stage) into
# the /usr/share/nginx/html folder:
COPY --from=builder /usr/src/dist /usr/share/nginx/html

# 4: Copy the nginx configuration:
ADD ./config/nginx.conf /etc/nginx/example.conf

# 5: Set `nginx` as the owner of the compiled app files, and change permissions
# on some folders:
RUN set -ex \
  && mkdir -p /var/cache/nginx/client_temp && chmod a+w /var/cache/nginx/client_temp \
  && mkdir -p /var/cache/nginx/proxy_temp && chmod a+w /var/cache/nginx/proxy_temp \
  && mkdir -p /var/cache/nginx/fastcgi_temp && chmod a+w /var/cache/nginx/fastcgi_temp

# 6: Add the entrypoint script:
ADD ./bin/entrypoint.sh /usr/local/bin/

# 7: Configure the image to use the entrypoint script:
# NOTE: Heroku has a bit of a problem parsing the ENTRYPOINT + CMD stuff, and only the "exec" form
# ('["executable", "param1", "param2"]' which is the preferred form) will work. Also, adding
# additional parameters in the ENTRYPOINT command are unlikely to work.
ENTRYPOINT [ "/usr/local/bin/entrypoint.sh" ]

# 8: Set the default command:
CMD [ "start" ]
