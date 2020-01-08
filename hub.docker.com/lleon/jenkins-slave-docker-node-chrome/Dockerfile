FROM gradiant/jenkins-slave-node-docker:latest

USER root


RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" | tee -a /etc/apt/sources.list \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -\
    && apt-get update \
    && apt-get install -y --no-install-recommends \
      google-chrome-stable \
  && apt-get autoremove -y \
  && rm -rf /var/lib/apt/lists/*

USER jenkins
