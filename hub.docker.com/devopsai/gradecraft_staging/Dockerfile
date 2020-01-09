# Gradecraft web application base image with secrets
# VERSION       2.0
# ENVIRONMENT	Staging

# ~~~~ Image base ~~~~
FROM ruby:2.5.3
MAINTAINER ai-devops <ai-devops@umich.edu>

# ~~~~ Newrelic ~~~~
RUN echo deb http://apt.newrelic.com/debian/ newrelic non-free >> /etc/apt/sources.list.d/newrelic.list
RUN wget -O- https://download.newrelic.com/548C16BF.gpg | apt-key add -
RUN wget -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | apt-key add -
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list

# ~~~~ Update OS ~~~~~
RUN apt-get update
RUN apt-get upgrade -y
RUN DEBIAN_FRONTEND=noninteractive apt-get install libssl1.0.2 libpq-dev wget git nginx vim newrelic-sysmond postgresql-client-9.5 libkrb5-dev nodejs krb5-user build-essential libfuse-dev libcurl4-openssl-dev libxml2-dev mime-support automake libtool wget tar zip cron -y

# ~~~~ Install S3 mount ~~~~~
RUN wget https://github.com/s3fs-fuse/s3fs-fuse/archive/v1.79.tar.gz -O /usr/src/v1.79.tar.gz
RUN tar xvz -C /usr/src -f /usr/src/v1.79.tar.gz
RUN cd /usr/src/s3fs-fuse-1.79 && ./autogen.sh && ./configure --prefix=/usr && make && make install
RUN mkdir /s3mnt
RUN chgrp -R 1000 /s3mnt
RUN chmod -R g+rwx /s3mnt

# ~~~~ Add non-root user ~~~~~
RUN useradd -l -u 1000690000 -s /bin/bash ocstag
#RUN printf "s3fs gc-archiver-staging /s3mnt">> /mounts3.sh
#RUN chmod +x /mounts3.sh

# ~~~~~ All environment variables ~~~~~
ENV RAILS_ENV staging
ENV MANDRILL_PASSWORD jL603d5PtE6rem-h25gA7w
ENV MANDRILL_USERNAME cholma@umich.edu
ENV NEW_RELIC_APP_NAME gradecraft-staging
ENV NEW_RELIC_LICENSE_KEY bb3a9789ef8a124ghf410f51286cc55188ed7a2d
ENV RACK_ENV staging
ENV RAILS_ENV staging
ENV RAILS_SECRET 8a1b99effc1c1d848e24cdc7f640e6b72834f204394c256813f987ffecb2cd75c3c3bb5fc5bbc29166344c75d04e470b61dd406c58080ebf14fa534b9d9b2476
ENV ROLLBAR_ENV staging
ENV ROLLBAR_CLIENT_TOKEN 8356b5dbb8a84c139197c6a3c3a2ee9d
ENV AWS_ACCESS_KEY_ID AKIAJMB7SAAYHI7PCA6A
ENV AWS_SECRET_ACCESS_KEY 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
ENV LTI_CONSUMER_KEY RJjLK6f9ghxy77J3FcKrtQ
ENV LTI_CONSUMER_SECRET i_3yxK7HJdrOYI45Tl7Q-AOdZBAbLDFS
ENV ROLLBAR_ACCESS_TOKEN ff1764fbc83f415a94515d930c570915
ENV REDIS_URL redis://gcredis-staging:6379
ENV PASSPHRASE 2746956502e2bf26412d57af257614d8
#ENV MEMCACHED_URL memcached-3.jxru4e.cfg.use2.cache.amazonaws.com:11211
ENV BACKUP_BUCKET hogwarts
ENV REDIS_HOST_IP gcredis-staging
ENV REDIS_PORT 6379
ENV CONSUMER_SERVICE_URL https://gradecraft-staging.ai.umich.edu/saml/consume
ENV LOGOUT_SERVICE_URL https://gradecraft-staging.ai.umich.edu/saml/logout
ENV IDP_ENTITY_ID https://shibboleth.umich.edu/idp/shibboleth
ENV IDP_SSO_TARGET_URL https://shibboleth.umich.edu/idp/profile/SAML2/Redirect/SSO
ENV IDP_SLO_TARGET_URL https://shibboleth.umich.edu/cgi-bin/logout?http://www.umich.edu/
ENV ISSUER https://gradecraft-staging.ai.umich.edu/saml/metadata
ENV LOGGLY_TOKEN dab0a78f-d41a-45da-af99-4d1489b5661a
ENV AWSACCESSKEYID AKIAJMB7SAAYHI7PCA6A
ENV AWSSECRETACCESSKEY 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
ENV TERM_CHILD 1
ENV AWS_S3_BUCKET gradecraft-staging
ENV AWS_REGION us-west-2
ENV AWS_S3_REGION us-east-1
ENV AWS_KMS_KEY_ID d5f6e694-b90e-4a5d-97f4-bb7d19ac7e17
ENV IDP_CERT /gradecraft/gradecraft_saml_idp.pem
ENV SAML_PR_KEY /gradecraft/gcstagingsha256.key
ENV SAML_CERT /gradecraft/gcstagingsha256.crt
ENV CANVAS_CLIENT_ID 17700000000000012
ENV CANVAS_CLIENT_SECRET MGmIzWfs01SIpOrqPSxlZvMJsOZTyBOaZZJsOPzDoS4nlfzfQZ95308trKXozT8M
ENV CANVAS_BASE_URL https://umich.instructure.com
ENV GOOGLE_CLIENT_ID 981160405042-nd5vcf1u04abmqqnb9egjt3h1lvqpapc.apps.googleusercontent.com
ENV GOOGLE_SECRET -rGEqrMB3-YvhrRH7NlxQJXU
ENV GMAIL_SMTP_USERNAME gc.staging@gmail.com
ENV GMAIL_SMTP_PASSWORD PiagetVygotskyBandura!
ENV MAIL_INTERCEPTOR_RECIPIENT gc.staging@gmail.com
ENV RECAPTCHA_SITE_KEY 6LciBk8UAAAAALIoo6dq6pZ8j-rTfd6mgzM4-SMb
ENV RECAPTCHA_SECRET_KEY 6LciBk8UAAAAAIm48KnXqCDrnVBE9DkFDY2N8TOq

# ~~~~ Adding some more secrets ~~~~
RUN mkdir /intermidiate
WORKDIR /intermidiate/
ADD gradecraft_saml_idp.pem /intermidiate/gradecraft_saml_idp.pem
ADD gcstagingsha256.key /intermidiate/gcstagingsha256.key
ADD gcstagingsha256.crt /intermidiate/gcstagingsha256.crt
ADD www.gradecraft.com.key /intermidiate/www.gradecraft.com.key
ADD www.gradecraft.com.crt /intermidiate/www.gradecraft.com.crt
ADD database.yml /intermidiate/database.yml
ADD mongoid.yml /intermidiate/mongoid.yml
ADD puma.rb /intermidiate/puma.rb
ADD Procfile /intermidiate/Procfile

# ~~~~ Add cron jobs ~~~~
ADD cron/crontab /etc/cron.d/trim-cron
RUN chmod 0644 /etc/cron.d/trim-cron
RUN touch /var/log/cron.log

# ~~~~~ Setting up Kerberos ~~~~~
RUN rm /etc/krb5.conf
RUN mkdir /etc/krb5kdc
ADD krb5.conf /etc/krb5.conf
ADD kdc.conf /etc/krb5kdc/kdc.conf
ADD default /etc/nginx/sites-available/default

# ~~~~~ Opening Ports ~~~~~
EXPOSE 8080
EXPOSE 8443
