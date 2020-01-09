FROM buildkite/agent:3-ubuntu

# set labels
LABEL maintainer="Nightah"

# set runtime variables
ENV GOROOT="/usr/local/go"
ENV GOPATH="/root/gopath"
ENV NVM_DIR="/root/.nvm"
ENV PATH="$PATH:/usr/local/go/bin"

# modifications
RUN \
 echo "**** Install Authelia CI pre-requisites ****" && \
   apt update -y && apt-get install -y -q gnupg2 && \
   curl -o- https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
   echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list && \
   apt update -y && apt install -y -q \
     build-essential google-chrome-stable libgif-dev nodejs unzip xvfb && \
  echo "**** Install Chromedriver ****" && \
     cd /tmp && \
     curl -o chromedriver_linux64.zip https://chromedriver.storage.googleapis.com/78.0.3904.105/chromedriver_linux64.zip && \
     unzip chromedriver_linux64.zip -d ./ && \
     mv -f chromedriver /usr/local/bin/chromedriver && \
     chmod +x /usr/local/bin/chromedriver && \
 echo "**** Install Golang ****" && \
   curl -o go1.13.5.linux-amd64.tar.gz https://dl.google.com/go/go1.13.5.linux-amd64.tar.gz && \
   tar -xf go1.13.5.linux-amd64.tar.gz && \
   mv go /usr/local && \
 echo "**** Install NVM ****" && \
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash && \
 echo "**** Cleanup ****" && \
   apt-get clean && \
   rm -rf \
     /tmp/* \
     /var/lib/apt/lists/* \
     /var/tmp/*
