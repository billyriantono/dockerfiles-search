FROM node:10.15.1

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
      echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
      apt-get update && \
      apt-get install -y google-chrome-stable xvfb

COPY set_umask.sh set_umask.sh
ENTRYPOINT ["/set_umask.sh"]
