FROM droptica/php-developer:7.1-v1.5

RUN echo "memory_limit = 2048M" > /usr/local/etc/php/conf.d/memory_limit.ini
RUN apt-get update && apt-get install --no-install-recommends -y openssh-client httrack zip
RUN composer self-update
RUN composer global require hirak/prestissimo
ADD .ssh/config /root/.ssh/config
RUN chmod 600 /root/.ssh/config
RUN chown root /root/.ssh/config

WORKDIR /app
