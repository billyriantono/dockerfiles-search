FROM gitlab/dind

RUN apt-get update && \
  apt-get install -y build-essential libfontconfig zip git apt-transport-https ca-certificates curl openssl software-properties-common && \
  curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
  apt-get install -y nodejs && \
  npm install grunt -g && \
  npm install grunt-cli -g && \
  npm install findup-sync resolve nopt -g && \
  node --version && \
  npm --version && \
  apt-get autoremove -y  

RUN apt-get update
RUN apt-get install -y build-essential
RUN npm install -g serverless
