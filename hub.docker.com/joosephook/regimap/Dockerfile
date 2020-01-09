FROM tutum/apache-php

RUN apt-get update && apt-get install -yq vim php5-sybase python
#python-opencv && rm -rf /var/lib/apt/lists/*
RUN rm -fr /app

COPY regilaul/ /app/regilaul/
COPY web_conf.php /app/regilaul/web_conf.php
#COPY regilaul/templ /app/templ
#RUN mv /app/regilaul/php1.00 /app/ && mv /app/regilaul/index.php /app/ && mv /app/regilaul/web_conf.php /app/
#ADD web_conf.php /app/
#ADD index.php /app/

# install sybase sql anywhere 12 client
ADD sqla1201_client_linux_x86x64.tar.gz /app/
RUN sudo /app/client1201/setup -silent -I_accept_the_license_agreement

RUN echo 'export PATH=$PATH:/opt/sqlanywhere12/lib64' >> /etc/apache2/envvars
# install php module
COPY php-5.5.0_sqlanywhere.so /usr/lib/

COPY sqlanywhere.ini /etc/php5/mods-available/sqlanywhere.ini

#RUN php5enmod sqlanywhere
RUN ln -s /etc/php5/mods-available/sqlanywhere.ini /etc/php5/apache2/conf.d/20-sqlanywhere.ini
RUN ln -s /etc/php5/mods-available/sqlanywhere.ini /etc/php5/cli/conf.d/20-sqlanywhere.ini


#RUN vim -c ':normal $i:/opt/sqlanywhere12/lib32' -c wq /etc/environment

COPY sqlanywhere.conf /etc/ld.so.conf.d/
RUN ldconfig
RUN ldconfig -p | grep libdbc
RUN touch /var/log/phperr.log && chown www-data:www-data /var/log/phperr.log && chmod 755 /var/log/phperr.log

#RUN sed -i 's/error_reporting =.*/error_reporting = E_ALL/g' /etc/php5/apache2/php.ini
#RUN sed -i 's/\(display_errors =\).*/\1 On/g' /etc/php5/apache2/php.ini
#RUN sed -i 's/\(display_startup_errors =\).*/\1 On/g' /etc/php5/apache2/php.ini
#RUN sed -i 's/;\(error_log =\).*/\1 \/var\/log\/phperr\.log/g' /etc/php5/apache2/php.ini
#RUN sed -i 's/;\(include_path =\).*/\1 ".:\/usr\/share\/php:\/app\/regilaul\/php1.00\/class:\/app\/regilaul\/php1.00\/module"/g' /etc/php5/apache2/php.ini
#RUN sed -i 's/\(HostnameLookups\).*/\1 On/g' /etc/apache2/apache2.conf
#RUN sed -i 's/\(doc_root =\).*/\1 \/app\/regilaul\//g' /etc/php5/apache2/php.ini

RUN echo 'extension=/usr/lib/php-5.5.0_sqlanywhere.so' >> /etc/php5/apache2/php.ini
RUN php5enmod sqlanywhere
RUN chmod -R 777 /app
RUN chmod -R 777 /var
RUN chmod -R 777 /var/

RUN a2enmod rewrite

RUN ln -s /app/regilaul/templ /usr/share/php/
RUN ln -s /app/regilaul/php1.00/ /usr/share/php/

#RUN cp -r regilaul/templ/ /usr/share/php/
#RUN cp -r regilaul/php1.00/class/* /usr/share/php/
#RUN cp -r regilaul/php1.00/module/* /usr/share/php/
#RUN cp -r regilaul/php1.00/smarty/* /usr/share/php/smarty/
#RUN cp -r regilaul/php1.00/*.php /usr/share/php/

RUN chmod -R 777 /app
RUN chown -R www-data:www-data /app/

COPY 000-default.conf /etc/apache2/sites-available
RUN a2dissite 000-default && a2ensite 000-default
RUN service apache2 restart
EXPOSE 80

CMD ["/usr/sbin/apachectl", "-D","FOREGROUND"]
