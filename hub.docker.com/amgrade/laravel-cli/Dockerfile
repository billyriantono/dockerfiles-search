FROM amgrade/phpcli

RUN apt-get -y update && \
    apt-get -y install curl && \
    curl -sL https://deb.nodesource.com/setup | bash -  && \
    apt-get install -y nodejs  && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get remove --purge curl -y  && \
    apt-get clean

RUN npm install -g bower gulp