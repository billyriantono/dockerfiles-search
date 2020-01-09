FROM ubuntu:18.04
MAINTAINER John Tashiro <jtashiro@fiospace.com>

RUN apt-get update
RUN apt-get install -y python libexpat1 apache2 apache2-utils ssl-cert libapache2-mod-wsgi \
	sqlite3 vim \
	python-setuptools python-dev build-essential python-pip

# python dependencies and dreamscreen
RUN pip install requests
RUN pip install flask
RUN pip install bs4
RUN pip install DreamScreenWeatherApp
# patch dreamscreen
COPY service.py /usr/local/lib/python2.7/dist-packages/DreamScreenWeatherApp/
COPY getForecastApi.html /usr/local/lib/python2.7/dist-packages/DreamScreenWeatherApp/templates/

# configure a test script
COPY wsgi_test_script.py /var/www/html/

# enable wsgi dreamscreen mappings for apache2 httpd
COPY mod-wsgi.conf  /etc/apache2/conf-available/
RUN a2enconf mod-wsgi 

# directories
#RUN mkdir -p /usr/var/service-instance
#RUN mkdir -p /usr/var/logs
#RUN chmod -R 777 /usr/var/logs
#RUN chmod -R 777 /usr/var/service-instance
#RUN chmod -R 777 /usr/var


# copy apache config
COPY apache2/ports.conf /etc/apache2/
COPY apache2/000-default.conf /etc/apache2/sites-enabled/
RUN chmod -R 777 /var/log/apache2
RUN chmod -R 777 /var/run/apache2


#RUN ls -la /var/log
#RUN chown www-data /usr/var/logs
#RUN chown www-data /etc/apache2
#RUN chmod 775 /var/log/apache2
#RUN chown -R www-data /var/log/apache2
#RUN chown www-data /var/run/apache2



COPY startup.sh /
RUN chmod +x /startup.sh

# fix up for heroku
CMD /startup.sh


