FROM wordpress

RUN apt-get update && apt-get install -y unzip

COPY . /usr/src

# execute package script inside the wordpress installation directory
WORKDIR /usr/src/wordpress
RUN /bin/sh -c ". /usr/src/scripts/package.sh"

# set workdir correctly for the execution of the entrypoint.sh as provided by the wordpress layer
WORKDIR /var/www/html

#su -c "php wp-cli.phar plugin install woocommerce" -s /bin/sh www-data 
# docker run --name wordpress-test --link some-mysql:mysql -p 80:80 -v "$PWD/wordpress":/var/www/html/wp-content -d ff18
# docker run --name wordpress-test --link some-mysql:mysql -p 80:80 -d rbergenl/wordpress
# docker exec -it wordpress-test bash