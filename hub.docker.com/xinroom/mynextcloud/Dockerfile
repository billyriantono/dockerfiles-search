FROM nextcloud:stable-fpm-alpine

COPY diy.sh /diy.sh

RUN chmod +x /diy.sh

ENTRYPOINT ["/diy.sh"]
CMD ["php-fpm"]