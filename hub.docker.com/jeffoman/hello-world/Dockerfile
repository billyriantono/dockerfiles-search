FROM alpine:latest 
LABEL maintainer="jeffoman" 
LABEL description="This example Dockerfile installs Apache & PHP." 

ENV PHPVERSION 7 

RUN apk add --update apache2 php${PHPVERSION}-apache2 php${PHPVERSION} && \
    rm -rf /var/cache/apk/* && \
    echo "<H1>HELLO WORLD ^_^</H1>" > /var/www/localhost/htdocs/index.html && \
    echo "<?php phpinfo(); ?>" > /var/www/localhost/htdocs/index.php && \
    chmod 755 /var/www/localhost/htdocs/index.php 

EXPOSE 80/tcp 

ENTRYPOINT ["httpd"] 
CMD ["-D", "FOREGROUND"]
