FROM alpine:3.6
LABEL name="Docker image for Twin synergy" \
    version="1.0.0" \
    org.label-schema.url="twinsynergy/deploy:latest" \
    org.label-schema.vcs-url="https://bitbucket.org/twinsyn/di-deploy/" \
    org.label-schema.vendor="Twin Synergy Co.Ltd"
RUN packages=' \
    openssh \
    sshpass \
    openssl \
    ' \
    set -x \
    && apk --update add $packages \
    && rm -rf /var/cache/apk/*