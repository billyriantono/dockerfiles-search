FROM silintl/apache2:latest

ENV REFRESHED_AT 2018-06-12

RUN apt-get update -y \
    && apt-get clean

COPY redirect.conf /etc/apache2/sites-enabled/
COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2ctl", "-D", "FOREGROUND"]
