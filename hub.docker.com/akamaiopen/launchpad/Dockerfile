ARG NODE_VERSION=10
FROM node:${NODE_VERSION}-alpine
WORKDIR /home/theia
ADD theia/package.json ./package.json
ADD theia/yarn.lock ./yarn.lock
ADD theia/akamai-theia-extension/akamai-extension ./akamai-extension
RUN apk update && \
    apk add --no-cache make gcc g++ python && \
    yarn --pure-lockfile && \
    NODE_OPTIONS="--max_old_space_size=4096" yarn theia build && \
    yarn --production && \
    yarn autoclean --init && \
    echo *.ts >> .yarnclean && \
    echo *.ts.map >> .yarnclean && \
    echo *.spec.* >> .yarnclean && \
    yarn autoclean --force && \
    yarn cache clean

FROM node:${NODE_VERSION}-alpine
ENV HOME=/home/launchpad SHELL=/bin/bash USE_LOCAL_GIT=true AKAMAI_CLI_HOME=/launchpad/cli GOROOT=/usr/lib/go GOPATH=/go PATH=/go/bin:$PATH JAVA_HOME=/usr/lib/jvm/default-jvm
RUN apk update && \
    apk add --no-cache \
    git \
    go \
    openssh \
    bash \
    python2 \
    python2-dev \
    py2-pip \
    python3 \
    python3-dev \
    wget \
    jq \
    openssl \
    openssl-dev \
    openjdk8 \
    curl \
    build-base \
    libffi \
    libffi-dev \
    vim \
    nano \
    util-linux \
    tree \
    bind-tools \
    libc6-compat \
    nss && \
    rm -f /var/cache/apk/* && \
    addgroup theia && \
    adduser -G theia -s /bin/sh -D theia && \
    addgroup launchpad && \
    adduser -G launchpad -s /bin/bash -D -h /launchpad launchpad && \
    chmod g+rw /home && \
    mkdir -p /go/bin && \
    mkdir -p /launchpad && \
    mkdir -p $HOME && \
    mkdir -p $AKAMAI_CLI_HOME/.akamai-cli

COPY --from=0 --chown=theia:theia /home/theia /home/theia

RUN if [[ ! -f /lib/ld-linux-x86-64.so.2 ]]; then ln -s /lib/libc.musl-x86_64.so.1 /lib/ld-linux-x86-64.so.2; fi
RUN wget -q `curl -s https://api.github.com/repos/akamai/cli/releases/latest | jq .assets[].browser_download_url | grep linuxamd64 | grep -v sig | sed s/\"//g`
RUN mv akamai-*-linuxamd64 /usr/local/bin/akamai && \
    chmod +x /usr/local/bin/akamai && \
    curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh && \
    go get github.com/akamai/cli && \
    cd $GOPATH/src/github.com/akamai/cli && \
    dep ensure && go build -o /usr/local/bin/akamai && \
    chmod +x /usr/local/bin/akamai && \
    pip3 install --upgrade pip && \
    pip3 install --upgrade httpie-edgegrid && \
    chown -R launchpad:launchpad $HOME && \
    chown -R launchpad:launchpad $AKAMAI_CLI_HOME && \
    chown -R launchpad:launchpad /home/theia

#ARG S3FS_VERSION="v1.85"
#RUN git clone https://github.com/s3fs-fuse/s3fs-fuse.git && \
#    cd s3fs-fuse && \
#    git checkout tags/${S3FS_VERSION} && \
#    ./autogen.sh && \
#    ./configure --prefix=/usr && \
#    make && \
#    make install && \
#    rm -rf /var/cache/apk/*

USER launchpad
RUN echo "[cli]" > $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo "cache-path            = ${AKAMAI_CLI_HOME}/.akamai-cli/cache" >> $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo "config-version        = 1.1" >> $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo "enable-cli-statistics = true" >> $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo "last-ping             = 2018-08-08T00:00:12Z" >> $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo "client-id             = launchpad" >> $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo "install-in-path       = no" >> $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo "last-upgrade-check    = ignore" >> $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo "stats-version         = 1.1" >> $AKAMAI_CLI_HOME/.akamai-cli/config && \
    echo '         ___    __                         _    ' >  $HOME/.motd && \
    echo '        /   |  / /______ _____ ___  ____ _(_)   ' >> $HOME/.motd && \
    echo '       / /| | / //_/ __ `/ __ `__ \/ __ `/ /    ' >> $HOME/.motd && \
    echo '      / ___ |/ ,< / /_/ / / / / / / /_/ / /     ' >> $HOME/.motd && \
    echo '     /_/  |_/_/|_|\__,_/_/ /_/ /_/\__,_/_/      ' >> $HOME/.motd && \
    echo '================================================' >> $HOME/.motd && \
    echo '=    Welcome to Launchpad Labs from Akamai     =' >> $HOME/.motd && \
    echo '================================================' >> $HOME/.motd && \
    echo 'eval "$(/usr/local/bin/akamai --bash)"' > $HOME/.bashrc && \
    echo "cat $HOME/.motd" >> $HOME/.bashrc && \
    echo "PS1='Akamai Developer [\w]$ '" >> $HOME/.bashrc && \
    mkdir $HOME/.httpie && \
    echo '{' > $HOME/.httpie/config.json && \
    echo '"__meta__": {' >> $HOME/.httpie/config.json && \
    echo '    "about": "HTTPie configuration file", ' >> $HOME/.httpie/config.json && \
    echo '    "httpie": "1.0.0-dev"' >> $HOME/.httpie/config.json && \
    echo '}, ' >> $HOME/.httpie/config.json && \
    echo '"default_options": ["--timeout=300","--style=autumn"], ' >> $HOME/.httpie/config.json && \
    echo '"implicit_content_type": "json"' >> $HOME/.httpie/config.json && \
    echo '}' >> $HOME/.httpie/config.json && \
    touch $HOME/.edgerc && \
    ln -s /cli /launchpad/cli && \
    ln -s $HOME/.edgerc /launchpad/.edgerc && \
    cd /launchpad && \
    git clone https://github.com/akamai/launchpad-labs-example-files examples && \
    mkdir /launchpad/cli/.akamai-cli/cache

RUN akamai install --force property property-manager api-gateway image-manager sandbox

#VOLUME /pipeline
WORKDIR /home/theia

#COPY ./entrypoint.sh /home/theia/bin/entrypoint.sh
#COPY ./passphrase.sh /home/theia/bin/passphrase.sh
#
#USER root
#RUN chmod +x /home/theia/bin/entrypoint.sh && \
#    chmod 777 /home/theia/bin/passphrase.sh && \
#    chown -R theia:theia /home/theia/bin && \
#    ln -s /home/theia/launchpad /launchpad

#USER theia

EXPOSE 3000 9550

#ENV AWS_ACCESS_KEY="QUtJQVNSS0RENFlST0c0VjdPTloK" AWS_SECRET_KEY="eGNoTW11NXVwRGNCT3AzVXA5ZmlCdEVSaDNvZWtzK29FVnltVTRpNgo="
#ENV AVL_STUDENT_ID="devnull3@akamaideveloper.com"
#ENTRYPOINT [ "/home/theia/bin/entrypoint.sh" ]
#CMD /bin/bash

ENTRYPOINT [ "node", "/home/theia/src-gen/backend/main.js", "/launchpad", "--hostname=0.0.0.0" ]