FROM alpine:3.8

RUN apk --no-cache add net-snmp=5.7.3-r11
RUN echo 'disableAuthorization yes' > /etc/snmp/snmptrapd.conf

VOLUME ["/etc/snmp/","/var/lib/net-snmp/","/root"]

EXPOSE 162

CMD ["snmptrapd","-L","o","-f","::","0.0.0.0"]
