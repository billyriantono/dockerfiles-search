FROM frolvlad/alpine-oraclejdk8:full
RUN apk add --update curl tzdata && \
    rm -rf /var/cache/apk/*
RUN cp /usr/share/zoneinfo/Australia/Sydney /etc/localtime && echo "Australia/Sydney" >  /etc/timezone 


