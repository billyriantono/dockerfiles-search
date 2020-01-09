# 1: Use ruby 2.3.1 as base:
FROM securable/backend-base-image

# 2: We'll set the application path as the working directory
WORKDIR /usr/src/app

# 3: We'll add the app's binaries path to $PATH:
ENV HOME=/usr/src/app PATH=/usr/src/app/bin:$PATH

ENV BUILD_PACKAGES="" \
 DEV_PACKAGES="libcairo2-dev libjpeg62-turbo-dev libpango1.0-dev libgif-dev build-essential g++" \
 SYSTEM_PACKAGES=""

RUN apt-get update \
  && apt-get install -y $BUILD_PACKAGES $SYSTEM_PACKAGES $DEV_PACKAGES \
  && rm -rf /var/lib/apt/lists/*

RUN npm install canvas \
  && npm install chart.js \
  && npm install chartjs-node

# 5: Install the current project gems - they can be safely changed later
# during development via `bundle install` or `bundle update`:
COPY . /usr/src/app/
RUN set -ex && bundle install

RUN RAILS_ENV=production

EXPOSE 3000
