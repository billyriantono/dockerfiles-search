FROM atmoz/sftp

RUN apt-get update \
    && apt-get install -y fail2ban \
    && cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local \
    && service fail2ban restart
