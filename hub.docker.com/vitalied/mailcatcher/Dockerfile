FROM ruby:alpine

ENV HTTP_PORT 1080
ENV SMTP_PORT 1025

EXPOSE $HTTP_PORT $SMTP_PORT

RUN apk add --no-cache g++ make musl-dev sqlite-libs sqlite-dev libstdc++ && \
    gem install --no-document mailcatcher && \
    apk del --purge g++ make musl-dev sqlite-dev

COPY run.sh /run.sh
RUN chmod +x /run.sh

CMD ["/run.sh"]
