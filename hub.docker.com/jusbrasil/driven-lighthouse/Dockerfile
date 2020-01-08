FROM node:10-slim

# See https://crbug.com/795759
RUN apt-get update --fix-missing && apt-get -y upgrade
RUN apt-get install -yq libgconf-2-4

# Install latest chrome dev package.
# Note: this installs the necessary libs to make the bundled version of Chromium that Puppeteer
# installs, work.
RUN apt-get update && apt-get install -y wget --no-install-recommends \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update \
    && apt-get install -y google-chrome-unstable --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get purge --auto-remove -y curl \
    && rm -rf /src/*.deb

ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 /usr/local/bin/dumb-init
RUN chmod +x /usr/local/bin/dumb-init

# Download latest Lighthouse from npm.
# cache bust so we always get the latest version of LH when building the image.
ARG CACHEBUST=1
RUN npm i lighthouse@5.0.0 -g

ENV app /usr/app
WORKDIR ${app}
COPY . ${app}

RUN yarn install
RUN yarn run build

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh

# Add user so we don't need --no-sandbox.
RUN groupadd -r chrome && useradd -r -g chrome -G audio,video chrome \
    && mkdir -p /home/chrome/Downloads \
    && mkdir /usr/app/reports \
    && chown -R chrome:chrome /home/chrome \
    && chown -R chrome:chrome /usr/app/reports \
    && chown -R chrome:chrome /usr/app/node_modules

# Run everything after as non-privileged user.
USER chrome

# Disable Lighthouse error reporting to prevent prompt.
ENV CI=true

EXPOSE 8080

ENTRYPOINT ["dumb-init", "--", "/entrypoint.sh"]
