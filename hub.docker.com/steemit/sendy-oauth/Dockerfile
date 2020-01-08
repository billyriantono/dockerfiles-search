FROM phusion/baseimage:0.9.19

RUN \
    apt-get update && \
    apt-get install -y \
        nginx \
        git \
        wget \
        gettext \
    && \
    apt-get clean

# retrieve latest version of go and build oauth2_proxy
RUN \
    mkdir goinstall && \
    cd goinstall && \
    wget https://storage.googleapis.com/golang/go1.11.2.linux-amd64.tar.gz && \
    tar -xvf go1.11.2.linux-amd64.tar.gz && \
    mv go /usr/local && \
    export GOROOT=/usr/local/go && \
    cd && \
    mkdir /usr/share/gobuild && \
    export GOPATH=/usr/share/gobuild && \
    export PATH=$GOROOT/bin:$PATH && \
    go get github.com/bitly/oauth2_proxy && \
    cp /usr/share/gobuild/bin/oauth2_proxy /usr/bin && \
    # remove build directory for golang (cleanup)
    rm -rf /usr/share/gobuild

#make nginx not run as a daemon so it doesn't exit at entrypoint
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

RUN mkdir /etc/oauth2_proxy

ADD authorizedemails /etc/oauth2_proxy/authorizedemails

ADD oauth2.config.template /etc/oauth2_proxy/oauth2.config.template

ADD startservices.sh /usr/bin/startservices.sh

RUN chmod +x /usr/bin/startservices.sh

ADD nginx.conf.template /etc/nginx/nginx.conf.template

CMD /usr/bin/startservices.sh
