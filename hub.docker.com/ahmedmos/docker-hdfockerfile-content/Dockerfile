FROM aerialtech/docker-alpine-aws-cli

RUN apk --update --no-cache add postgresql \
    && rm -rf /var/cache/apk/* /root/.cache/pip/* /usr/lib/python2.7/site-packages/awscli/examples
