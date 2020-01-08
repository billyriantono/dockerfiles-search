FROM php:7.2-alpine

LABEL maintainer="rodolphe@eveilleau.fr"

RUN apk update \                                                                                                                                                                                                                        
 && apk add ca-certificates wget \                                                                                                                                                                                                      
 && update-ca-certificates   

RUN wget https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar \
 && wget https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar     

RUN chmod +x phpcs.phar \
 && mv phpcs.phar /usr/bin/phpcs

RUN chmod +x phpcbf.phar \
 && mv phpcbf.phar /usr/bin/phpcbf

ENTRYPOINT [""]

CMD ["phpcs --help"]
