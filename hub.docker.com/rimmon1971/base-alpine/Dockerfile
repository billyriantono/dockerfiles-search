FROM alpine:3.7
LABEL osname="Alpine Linux"
LABEL osversion="3.7" 
LABEL build-date="20180228"
LABEL maintainer="Ferdinando Simonetti <ferdinando.simonetti@outlook.com>"
# build-time proxy settings
ARG MYPROXY
ARG NOPROXY
ENV http_proxy $MYPROXY
ENV https_proxy $MYPROXY
ENV no_proxy $NOPROXY
ENV HTTP_PROXY $MYPROXY
ENV HTTPS_PROXY $MYPROXY
ENV NO_PROXY $NOPROXY

RUN apk --no-cache update && apk --no-cache upgrade

CMD ["/bin/sh"]
