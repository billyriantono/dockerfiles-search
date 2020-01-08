FROM alpine:3.11.2

RUN apk add --update --no-cache \
            supervisor
            
RUN mkdir /etc/supervisord.d

ADD fs/etc/supervisord.conf /etc/supervisord.conf
ADD fs/etc/supervisord.d/* /etc/supervisord.d/

ADD fs/setup-and-run.sh /setup-and-run.sh 
RUN chmod +x /setup-and-run.sh

ENTRYPOINT [ "/setup-and-run.sh" ]
