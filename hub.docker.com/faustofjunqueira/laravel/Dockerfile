FROM faustofjunqueira/apache2

MAINTAINER Fausto Junqueira "faustoferjunqueira@gmail.com"

RUN apt-get install curl -yf

WORKDIR /tmp

RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer

RUN chmod +x composer

RUN cp composer /usr/bin/composer

RUN rm composer

VOLUME ["/shared"]

CMD ["/bin/bash"]