FROM ruby:2.5.3-alpine3.8
RUN  apk -v --update add python                   \
                         py-pip                   \
                         groff                    \
                         less                     \
                         mailcap                  \
         && pip install --upgrade awscli==1.16.52 \
         && apk -v --purge del py-pip             \
         && rm /var/cache/apk/*

VOLUME /root/.aws

