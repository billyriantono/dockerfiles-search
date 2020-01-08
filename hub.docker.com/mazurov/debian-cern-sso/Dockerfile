FROM jtgasper3/debian-shibboleth-sp

RUN apt-get update \
	&& apt-get -y install curl \
	&& apt-get clean

RUN ln -s /usr/lib/apache2/modules/ /etc/apache2/modules \
    && ln -s /var/run/apache2 /etc/apache2/run

RUN cd /etc/shibboleth/ \
    && shib-keygen -f

RUN curl -sLo /usr/local/bin/ep https://github.com/kreuzwerker/envplate/releases/download/v0.0.7/ep-linux \
    && chmod +x /usr/local/bin/ep

ADD files/shibd /etc/shibboleth
COPY files/apache/apache2.conf /etc/apache2/apache2.conf
COPY files/www/ /var/www/html/

ENV APP_HOST localhost

VOLUME ["/var/www/html"]
CMD ["/usr/local/bin/ep", "-v", "/etc/apache2/apache2.conf", "/etc/shibboleth/shibboleth2.xml", "--", "/usr/local/bin/httpd-foreground"]