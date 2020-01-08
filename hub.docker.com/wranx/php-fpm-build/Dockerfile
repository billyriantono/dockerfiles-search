FROM wranx/php-fpm-runtime:0.2.0

#Install Core Build
RUN apt-get update && apt-get install -y software-properties-common
RUN apt-get update && apt-get -y install curl
RUN (curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash) && \
    apt-get install -y git-lfs
RUN apt-get update && \
    apt-get install -y ant ant-contrib
RUN apt-get update && \
    apt-get install -y unzip && \
    apt-get install -y python-dev && \
    curl https://s3.amazonaws.com/aws-cli/awscli-bundle.zip -o /tmp/awscli-bundle.zip && \
    cd /tmp && \
    unzip awscli-bundle.zip && \
    ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
RUN apt-get update && \
    apt-get -y install jq gettext-base chromedriver
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs
RUN npm install -g s3-website
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn
RUN curl -L https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.3.0.1492.zip -o /opt/sonar-scanner.zip && \
    cd /opt && \
    unzip sonar-scanner.zip && \
    ln -s sonar-scanner-3.3.0.1492 sonar-scanner && \
    rm sonar-scanner.zip


#Install PHP build additional
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
