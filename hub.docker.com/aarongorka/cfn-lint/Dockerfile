FROM node:alpine
ENV CFN_LINT_VERSION 1.6.0
RUN apk add --no-cache git make
RUN yarn global add cfn-lint@${CFN_LINT_VERSION}
WORKDIR /srv/app
ENTRYPOINT ["cfn-lint"]
CMD []
