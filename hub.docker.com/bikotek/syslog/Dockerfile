FROM ubuntu 

MAINTAINER Unai Bikotek

RUN apt-get update

RUN apt-get install -y rsyslog curl swatch

RUN # provides UDP syslog reception
RUN echo 'module(load="imudp")' >> /etc/rsyslog.conf
RUN echo 'input(type="imudp" port="514")' >> /etc/rsyslog.conf
RUN # provides TCP syslog reception
RUN echo 'module(load="imtcp")' >> /etc/rsyslog.conf
RUN echo 'input(type="imtcp" port="514")' >> /etc/rsyslog.conf

RUN echo '$template TmplAuth, "/var/log/rsyslog/%HOSTNAME%/%PROGRAMNAME%.log"' >>  /etc/rsyslog.d/50-default.conf
RUN echo '$template TmplMsg, "/var/log/rsyslog/%HOSTNAME%/%PROGRAMNAME%.log"' >>  /etc/rsyslog.d/50-default.conf
RUN echo 'authpriv.*   ?TmplAuth' >>  /etc/rsyslog.d/50-default.conf
RUN echo '*.info,mail.none,authpriv.none,cron.none   ?TmplMsg' >>  /etc/rsyslog.d/50-default.conf

RUN mkdir /var/log/rsyslog

RUN chown syslog:syslog /var/log/rsyslog/

RUN echo "# watch for error" > /etc/swatch.conf
RUN echo "watchfor /firewall/" >> /etc/swatch.conf
RUN echo "        echo" >> /etc/swatch.conf
RUN echo "        exec = sh /slack-syslog.sh "$_"" >> /etc/swatch.conf

ADD start.sh /bin
RUN /bin/chmod +x /bin/start.sh

EXPOSE 514 514/udp

CMD []
ENTRYPOINT ["/bin/start.sh"]
