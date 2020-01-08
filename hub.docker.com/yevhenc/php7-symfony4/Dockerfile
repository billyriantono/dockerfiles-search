FROM php:7.2-fpm

ENV TIMEZONE="Europe/Kiev"
ENV UID=1002

RUN groupadd -g ${UID} dev
RUN useradd -m -r -g ${UID} -u ${UID} dev

ENTRYPOINT ["/usr/local/bin/fixuid"]

ADD ./fixuid /usr/local/bin/
RUN chmod +x /usr/local/bin/fixuid

# Done installing
WORKDIR /var/www/symfony
