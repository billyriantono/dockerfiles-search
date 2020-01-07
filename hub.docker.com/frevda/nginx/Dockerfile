FROM nginx:1.13.1
MAINTAINER frederic@vandenameele.net
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./fastcgi.conf /etc/nginx/fastcgi.conf
COPY ./vhostnl.conf /etc/nginx/sites-available/nl.photostock.express.live.conf
COPY ./vhostfr.conf /etc/nginx/sites-available/fr.photostock.express.live.conf
#RUN mkdir /var/www/appworx.net/public_html
#RUN chown -R www-data:www-data /var/www/appworx.net/public_html
#RUN rm /etc/nginx/conf.d/default.conf
RUN mkdir /etc/nginx/sites-enabled
RUN ln -s /etc/nginx/sites-available/nl.photostock.express.live.conf /etc/nginx/sites-enabled/
RUN ln -s /etc/nginx/sites-available/fr.photostock.express.live.conf /etc/nginx/sites-enabled/