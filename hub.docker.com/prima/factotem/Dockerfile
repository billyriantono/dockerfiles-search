FROM node:10.15.3

# TZ: https://github.com/primait/board/issues/1631
ENV TZ=:/etc/localtime

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -qqy unzip \
                     libncurses5 \
                     groff \
                     less \
                     awscli \
                     curl \
                     tar \
                     gzip \
                     vim \
                     tzdata \
                     python2.7 \
                     python-pip \
                     pkg-config \
                     libpcre++-dev \
                     apt-transport-https \
                     dumb-init && \
    pip install awscli && \
    echo "Etc/UTC" > /etc/timezone && \
    apt-get purge -y unzip \
                    wget && \
    rm -r /var/lib/apt/lists/* && \
    aws configure set default.s3.signature_version s3v4 && \
    aws configure set default.region eu-west-1 && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get -qqy install yarn && \
    rm -rf /var/lib/apt/lists/* && \
    yarn --version && \
    chown node:node /usr/local/bin && \
    cd /opt && \
    curl -sLO https://github.com/dcoker/biscuit/releases/download/v0.1.3/biscuit-linux_amd64.tgz && \
    tar xzvf biscuit-linux_amd64.tgz && \
    mv biscuit /usr/bin/biscuit && \
    chmod +x /usr/bin/biscuit && \
    rm biscuit-linux_amd64.tgz

COPY files/entrypoint.sh /entrypoint.sh

WORKDIR /code

ENTRYPOINT ["/entrypoint.sh"]

CMD ["nginx", "-g", "daemon off;"]
