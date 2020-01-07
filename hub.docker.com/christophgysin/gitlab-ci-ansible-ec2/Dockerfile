FROM alpine

RUN apk update \
    && apk add ansible openssh-client py-boto py-pip \
    && pip install boto3 \
    && rm /var/cache/apk/*

ADD https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py \
    /usr/bin/ansible-ec2.py

RUN chmod +x /usr/bin/ansible-ec2.py

ENTRYPOINT []
