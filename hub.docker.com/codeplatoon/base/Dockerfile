FROM python:3.8.0-buster

RUN curl -sL https://deb.nodesource.com/setup_13.x | bash - && \
  curl https://cli-assets.heroku.com/install.sh | sh && \
  apt-get update && \
  apt-get install -y --no-install-recommends \
    git \
    nodejs \
    postgresql \
    postgresql-client

WORKDIR /usr/local/src/code_platoon

COPY ./ ./
COPY .bashrc /root/.bashrc

CMD bash
