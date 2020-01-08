FROM    alpine:3.10.3
RUN     apk --update --no-cache add python py-pip groff less mailcap \
        && pip install --upgrade awscli==1.16.306 s3cmd==2.0.2 python-magic \
        && apk --purge del py-pip
VOLUME  /root/.aws
