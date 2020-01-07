FROM library/debian

RUN      apt-get update \
             &&    apt-get install -y wget gnupg2 \
             &&    wget -qO- https://deb.nodesource.com/setup_8.x | bash - \
             &&    apt-get install -y nodejs \
             &&    npm install -g cnpm --registry=https://registry.npm.taobao.org \
             &&    npm install -g @angular/cli
