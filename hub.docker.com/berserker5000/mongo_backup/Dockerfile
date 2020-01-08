FROM alpine:3.7

#ENV TZ=CEST
ENV TZ=Europe/Kiev

RUN apk add --no-cache mongodb-tools py2-pip && \
  pip install pymongo && \
  mkdir /backup && \
  mkdir /m_backup

COPY entrypoint.sh /usr/local/bin/entrypoint
COPY backup.sh /usr/local/bin/backup
COPY mongouri.py /usr/local/bin/mongouri

VOLUME /backup

CMD /usr/local/bin/entrypoint
