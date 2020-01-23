FROM alpine:3.2

# both groff and less are for `help` subcommands
RUN apk add --update python py-pip groff less \
 && pip install awscli             \
 && rm -rf /usr/lib/python2.7/distutils  \
       /usr/lib/python2.7/idlelib    \
       /usr/lib/python2.7/lib-tk     \
       /usr/lib/python2.7/ensurepip  \
       /usr/lib/python2.7/pydoc_data \
       /var/cache/apk/*

LABEL io.whalebrew.name aws
LABEL io.whalebrew.config.environment '["AWS_ACCESS_KEY_ID", "AWS_SECRET_ACCESS_KEY", "AWS_DEFAULT_REGION"]'
LABEL io.whalebrew.config.volumes '["~/.aws:/.aws"]'
LABEL io.whalebrew.config.networks '["host"]'

VOLUME ["/.aws"]

ENTRYPOINT ["aws"]
