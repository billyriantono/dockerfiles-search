FROM endotronic/guacamole:xenial

RUN \
  apt-get update && \
  apt-get install -y wget && \
  wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
  apt-get update && \
  apt-get install -y google-chrome-stable && \
  rm -rf /var/lib/apt/lists/*

RUN \
  mkdir /home/foo/chrome && \
  chown -R foo:foo /home/foo

CMD ["google-chrome", "--no-sandbox", "--user-data-dir=/home/foo/chrome"]
