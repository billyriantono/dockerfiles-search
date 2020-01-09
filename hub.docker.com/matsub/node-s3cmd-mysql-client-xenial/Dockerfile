FROM ubuntu:16.04
ENV DEBIAN_FRONTEND noninteractive

# install nodejs: https://github.com/nodesource/distributions/blob/master/README.md
RUN apt-get update && apt-get install -y \
        curl \
        mysql-client \
        git \
        s3cmd \
        && curl -sL https://deb.nodesource.com/setup_10.x | bash - \
        && apt-get install -y nodejs \
        && apt-get -yqq autoremove \
        && apt-get -y clean \
        && rm -rf /var/lib/apt/lists/*

# install dockerize: https://github.com/jwilder/dockerize#ubuntu-images<Paste>
ENV DOCKERIZE_VERSION v0.6.1
RUN curl -LO https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
        && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
        && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

CMD ["/bin/bash"]
