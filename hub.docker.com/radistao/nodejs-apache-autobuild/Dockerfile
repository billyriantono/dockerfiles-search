FROM ubuntu:latest
RUN apt-get -y update && apt-get install -y \
    nodejs \
    npm \
    apache2 \
    less

RUN apt-get clean

RUN rm -rf /var/lib/apt/lists/*

RUN a2enmod ssl && \
    a2ensite default-ssl

EXPOSE 80 433

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

#ENTRYPOINT /bin/bash
