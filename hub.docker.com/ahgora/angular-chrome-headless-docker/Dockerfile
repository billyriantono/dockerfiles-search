FROM debian:stable-slim

RUN apt update
RUN apt install -yy wget curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
	apt update && apt install -y nodejs
RUN node -v && npm -v

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
  apt update && apt install -y google-chrome-stable xvfb procps
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*
