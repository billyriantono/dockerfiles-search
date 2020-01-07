FROM alpine:3.6
LABEL maintainer="Steven Munro (stevenmunro at me dot com)"

### Set Defaults
    ENV DEBUG_MODE=FALSE \
        ENABLE_CRON=TRUE \
        ENABLE_SMTP=TRUE

### Set Defaults/Arguments
    ARG S6_OVERLAY_VERSION=v1.21.1.1 
    ARG MAJOR_VERSION=3.6


### Install MailHog
    RUN apk update && \
    apk --no-cache add --virtual mailhog-build-dependencies \
                go \
                git \
                musl-dev \
                && \
       mkdir -p /usr/src/gocode && \
       export GOPATH=/usr/src/gocode && \
       go get github.com/mailhog/MailHog && \
       go get github.com/mailhog/mhsendmail && \
       mv /usr/src/gocode/bin/MailHog /usr/local/bin && \
       mv /usr/src/gocode/bin/mhsendmail /usr/local/bin && \
       rm -rf /usr/src/gocode && \
       apk del --purge mailhog-build-dependencies && \
       adduser -D -u 1025 mailhog && \

### Add Core Utils
       apk upgrade && \
       apk add \
            bash \
            curl \
            less \
            logrotate \
            msmtp \
            nano \
            htop \
            tar \
            tzdata \
            vim \
            && \
       rm -rf /var/cache/apk/* && \
       rm -rf /etc/logrotate.d/acpid && \
       cp -R /usr/share/zoneinfo/Pacific/Auckland /etc/localtime && \
       echo 'Pacific/Auckland' > /etc/timezone && \

### S6 Installation
       curl -sSL https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz | tar xfz - -C / && \
   
### Add Folders
       mkdir -p /assets/cron

   ADD /install /

### Networking Configuration
   EXPOSE 1025 8025 10050/TCP 

### Entrypoint Configuration
   ENTRYPOINT ["/init"]
