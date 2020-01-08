FROM wranx/php-runtime:latest

RUN apt-get update && apt-get install -y ant
RUN (curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash) && \
    apt-get install -y git-lfs
RUN apt-get update && \
    apt-get install -y unzip && \
    apt-get install -y python-dev && \
    curl https://s3.amazonaws.com/aws-cli/awscli-bundle.zip -o /tmp/awscli-bundle.zip && \
    cd /tmp && \
    unzip awscli-bundle.zip && \
    ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
RUN apt-get update && \
    apt-get -y install jq

RUN apt-get update && \
    apt-get -y install postgresql

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer


