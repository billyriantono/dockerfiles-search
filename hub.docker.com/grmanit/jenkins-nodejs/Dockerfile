FROM grmanit/jenkins-base

# the nodesource setup script already runs apt-get update
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - &&\
    apt-get install -y nodejs build-essential && rm -rf /var/lib/apt/lists/* &&\
    npm install -g bower gulp angular-cli
