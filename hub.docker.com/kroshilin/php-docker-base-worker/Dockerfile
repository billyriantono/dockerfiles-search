FROM kroshilin/php-docker-base
ADD run.sh /etc/app/run.sh
WORKDIR /var/www
ENTRYPOINT ["/bin/bash", "/etc/app/run.sh"]
CMD ["echo", "Provide command"]