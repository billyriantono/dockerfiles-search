FROM alpine:3.8
RUN apk update
RUN apk add py-pip sudo curl
RUN pip install https://github.com/indigo-dc/udocker/archive/v1.1.3.tar.gz

ENV user udocker
RUN adduser -u 10004 -g 10000 -h /home/$user -D -s /bin/sh $user
RUN echo "$user ALL=(root) NOPASSWD:ALL" >> /etc/sudoers

USER $user
WORKDIR /home/$user
RUN udocker help
