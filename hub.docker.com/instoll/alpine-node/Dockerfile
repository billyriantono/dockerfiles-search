FROM alpine:3.4

RUN apk add --update --no-cache nodejs rsync tree vim jq zip build-base tar ca-certificates openssl bash && \
    update-ca-certificates && \
    echo "Install Spy filewatcher" && \
    cd /tmp && \
    wget -q https://github.com/jpillora/spy/releases/download/1.0.1/spy_1.0.1_linux_amd64.tar.gz && \
    tar xzf spy_1.0.1_linux_amd64.tar.gz && \
    mv spy_1.0.1_linux_amd64/spy /usr/bin && \
    rm -Rf spy_1.0.1_linux_amd64* && \
    echo "Install yarn" && \
    npm config set registry http://registry.npmjs.org && \
    npm install --silent -g yarn
