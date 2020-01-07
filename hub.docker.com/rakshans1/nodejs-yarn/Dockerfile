FROM rakshans1/nodejs

LABEL MAINTAINER="Rakshan Shetty <shetty.raxx555@gmail.com>"

WORKDIR "/opt/node"



RUN apt-get -qq update && apt-get -qq install -y curl git ca-certificates apt-transport-https --no-install-recommends && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean


