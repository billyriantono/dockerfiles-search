FROM library/ubuntu

#Install SFDX CLI
RUN apt-get update && \
    apt-get -y install wget && \
    apt-get -y install xz-utils curl gnupg2 openssl libssl-dev git unzip && \
    cd ~ && \
    wget https://developer.salesforce.com/media/salesforce-cli/sfdx-linux-amd64.tar.xz -O sfdx.tar.xz && \
    tar -xJf ~/sfdx.tar.xz && \
    cd sfdx* && \
    ./install
    



RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
     apt-get install -yq jq nodejs build-essential;

RUN npm install -g npm;

#RUN sfdx plugins:install sfdx-hydrate;