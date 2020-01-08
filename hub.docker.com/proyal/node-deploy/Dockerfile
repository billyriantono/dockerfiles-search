FROM node:10-alpine

RUN apk update
RUN apk -v --no-cache add bash git zip rsync openssh-client groff less python py-pip
RUN pip install awscli
RUN apk --purge -v del py-pip
