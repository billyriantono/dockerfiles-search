# ==============================================================================
# Dockerfile
# ==============================================================================
FROM ruby:2.5-slim-stretch
ENV LANG C.UTF-8

RUN apt update && apt install -y --no-install-recommends nodejs libpq-dev make gcc git curl g++ && \
  apt clean && apt autoremove && \
  rm -rf /var/lib/apt/lists/* && \
  curl https://cli-assets.heroku.com/install.sh | sh
