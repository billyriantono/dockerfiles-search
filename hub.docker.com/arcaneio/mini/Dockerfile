FROM alpine

RUN apk add --update --no-cache \
            bash \
            supervisor
            
RUN mkdir /etc/supervisord.d

ADD fs/etc/supervisord.conf /etc/supervisord.conf
ADD fs/etc/supervisord.d/* /etc/supervisord.d/

ADD fs/setup-and-run.sh /setup-and-run.sh 
RUN chmod +x /setup-and-run.sh

ENTRYPOINT [ "/setup-and-run.sh" ]
