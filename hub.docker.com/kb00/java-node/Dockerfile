FROM openjdk:8-jdk
MAINTAINER Kirill Bychkov <kb@na.ru>

RUN apt-get update -qq && apt-get install -qq --no-install-recommends \
  bash curl gnupg2

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update -qq && apt-get install -qq --no-install-recommends \
  nodejs yarn \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*