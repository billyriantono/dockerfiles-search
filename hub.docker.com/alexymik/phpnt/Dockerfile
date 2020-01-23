# Environement variables expected: 
# for webdav connection: WEBDAV_URL, WEBDAV_USER, WEBDAV_PASS
# for email sending: SERVICE_EMAIL, SERVICE_EMAIL_PASS
# for DB connection: MONGO_CONN_STRING

FROM python:3.6-alpine

WORKDIR /app/data/

ADD requirements.txt /app/

# Davfs2 needed to mount Yandex.Disk folder via WebDav protocol.
# For proper functioning 'use_locks 0' and 'delay_upload 0'
# flags need to be disabled.

RUN \
    apk update && apk upgrade &&                                          \
    apk --no-cache add davfs2 openssl ca-certificates py-openssl libffi-dev openssl-dev python-dev py-pip build-base &&  \
    pip3 install --upgrade pip && \
    pip3 install --no-cache-dir -r /app/requirements.txt  &&       \
    echo use_locks 0 >> /etc/davfs2/davfs2.conf &&                        \
    echo delay_upload 0 >> /etc/davfs2/davfs2.conf

ADD . /app/

CMD \
    echo $WEBDAV_URL $WEBDAV_USER $WEBDAV_PASS > /etc/davfs2/secrets &&   \
    mount -t davfs $WEBDAV_URL /app/data &&                               \
    cd /app && python3 main.py
