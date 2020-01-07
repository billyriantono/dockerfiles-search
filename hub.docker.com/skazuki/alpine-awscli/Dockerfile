FROM skazuki/alpine

LABEL maintainer="S-Kazuki<contact@revoneo.com>"

RUN apk --no-cache add bash curl less groff jq git python py-pip py2-pip zip \
&& pip install --upgrade pip awscli s3cmd \
&& mkdir /root/.aws