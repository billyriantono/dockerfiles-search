FROM wordpress

RUN apt-get update
RUN apt-get install unzip

WORKDIR /usr/src/wordpress/wp-content/plugins

ADD https://github.com/wp-graphql/wp-graphql/archive/v0.3.2.zip wp-graphql.zip
RUN unzip wp-graphql.zip
RUN mv wp-graphql-* wp-graphql

COPY wp-graphql-acf.zip .
RUN unzip wp-graphql-acf.zip

ADD https://downloads.wordpress.org/plugin/jonradio-private-site.2.14.2.zip private-site.zip
RUN unzip private-site.zip

ADD https://downloads.wordpress.org/plugin/wp-stateless.2.2.6.zip wp-stateless.zip
RUN unzip wp-stateless.zip

COPY acf.zip .
RUN unzip acf.zip

COPY srnd-announcements.php .

RUN rm *.zip

WORKDIR /var/www/html
