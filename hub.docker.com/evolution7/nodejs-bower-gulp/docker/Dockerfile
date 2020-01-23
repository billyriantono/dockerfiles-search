FROM debian:buster-slim

ENV SMTP_HOSTNAME smtp.example.com
ENV SMTP_RELAY relay.server.example.com
ENV SMTP_DOMAIN example.com
ENV SMTP_ORIGIN example.com
ENV SMTP_USER smtpuser
ENV SMTP_PASSWORD changeme

RUN apt-get update -y && apt-get dist-upgrade -y
RUN apt-get install postfix sasl2-bin rsyslog -y

# Set up saslauth
RUN sed -i "s/START=no/START=yes/" /etc/default/saslauthd
RUN perl -p -i -e "s|(?<=MECHANISMS=).*|\"shadow\"|" /etc/default/saslauthd
RUN perl -p -i -e "s|(?<=OPTIONS=).*|\"-c -m /var/spool/postfix/var/run/saslauthd\"|" /etc/default/saslauthd
RUN printf "pwcheck_method: saslauthd\nmech_list: PLAIN LOGIN\n" > /etc/postfix/sasl/smtpd.conf
RUN cp -f /etc/services /var/spool/postfix/etc/services

# Set up postfix
RUN perl -p -i -e "s|(?<=inet_protocols = ).*|ipv4|" /etc/postfix/main.cf

# Set up postfix to use saslauth
RUN printf "\nsmtpd_sasl_path = smtpd\n" >> /etc/postfix/main.cf
RUN echo "smtpd_sasl_type = cyrus" >> /etc/postfix/main.cf
RUN echo "smtpd_sasl_auth_enable = yes" >> /etc/postfix/main.cf
RUN echo "smtpd_sasl_security_options = noanonymous" >> /etc/postfix/main.cf

RUN usermod -aG sasl postfix

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh

EXPOSE 25
ENTRYPOINT ["/bin/bash", "/docker-entrypoint.sh"]
CMD ["/usr/bin/tail", "-f", "/var/log/mail.log"]
