FROM arwineap/docker-headless-chrome:latest

RUN apt-get update \
    && apt-get install -y ruby ruby-dev zlib1g-dev liblzma-dev build-essential git expect-dev \
    && rm -rf /var/lib/apt/lists/* \
    && gem install nokogiri \
    && gem install bundler
