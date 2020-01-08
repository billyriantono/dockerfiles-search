FROM node:12-alpine

# Set timezone to UTC by default
RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime

RUN apk update \
 && apk add \
   bash \
   make \
   curl \
   wget \
   openssh \
   git \
   less \
   python \
   py-pip \
 && pip install awscli \ 
 && apk --purge -v del py-pip \
 && rm /var/cache/apk/*

CMD ["/bin/bash"] 
