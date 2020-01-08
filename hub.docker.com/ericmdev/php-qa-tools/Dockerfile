# Debian: PHP QA Tools
#
# VERSION 0.0.1

# Pull the base image.
FROM ericmdev/php5

# Set the author.
MAINTAINER Eric Mugerwa <dev@ericmugerwa.com>

# Acquire tools.
RUN wget -c http://www.phpdoc.org/phpDocumentor.phar \
			-P /bin/
RUN wget -c https://phar.phpunit.de/phpcpd.phar \
			-P /bin/
RUN wget -c https://phar.phpunit.de/phploc.phar \
			-P /bin/ && \
			chmod +x /bin/phploc.phar
RUN wget -c http://static.phpmd.org/php/latest/phpmd.phar \
			-P /bin/
RUN wget -c http://static.pdepend.org/php/latest/pdepend.phar \
			-P /bin/
RUN wget -c https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar \
			-P /bin/
RUN wget -c https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar \
			-P /bin/
RUN wget -c https://github.com/bytepark/php-phar-qatools/raw/master/phpcb.phar \
			-P /bin/
RUN wget -c https://phar.phpunit.de/phpunit.phar \
			-P /bin/

# Add scripts.
ADD ./bin/ /bin

# Configure executable.
ENTRYPOINT ["sh", "/bin/start.sh"]

# Define default command.
CMD []