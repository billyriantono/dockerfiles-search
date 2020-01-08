FROM debian:stable-slim

ENV NG_CLI_ANALYTICS=ci
RUN export NG_CLI_ANALYTICS=ci
RUN apt-get update
RUN apt-get install -y wget curl gnupg git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
	apt-get update && apt-get install -y nodejs && \
	npm i -g npm@6

RUN node -v && npm -v

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
  apt-get update && \
  apt-get install -y google-chrome-stable xvfb
RUN google-chrome-stable --version
RUN apt update && apt install -y procps
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*