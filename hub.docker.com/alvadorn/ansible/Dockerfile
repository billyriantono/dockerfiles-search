#FROM python:3.7-alpine
FROM alpine:3.8

MAINTAINER "Igor Sant'ana <contato@igorsantana.com>"

# install updates
RUN apk --no-cache add ansible \
  rsync \
  openssh

CMD ["ansible-playbook"]



