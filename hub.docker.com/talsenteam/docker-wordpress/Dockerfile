FROM wordpress:php7.3-apache

COPY ./rootfs/ /

ENTRYPOINT [ "/bin/bash", "/opt/server--wordpress/entrypoint.sh" ]

CMD [ "apache2-foreground" ]
