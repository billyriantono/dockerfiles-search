FROM alpine:3.6

LABEL maintainer="Ivor Hung <ivor911@gmail.com>"

RUN apk add --no-cache apache2 && \
    mkdir -p /run/apache2 && \
    echo "<html><h1>Copy from Docker Cookbook</h1> <h1> 20200114-2, A new Hello World html file.</h1></html>" > \
        /var/www/localhost/htdocs/index.html

EXPOSE 80

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
