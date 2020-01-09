FROM fedora:21

RUN yum -y install openssl opensmtpd && yum clean all
RUN /bin/echo -e 'listen on 0.0.0.0\naccept from any for any relay' > /etc/opensmtpd/smtpd.conf
EXPOSE 25
ENTRYPOINT [ "smtpd", "-d" ]
