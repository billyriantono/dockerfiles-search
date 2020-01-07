FROM httpd:2.4
ADD apache/httpd.conf /usr/local/apache2/conf/
RUN mkdir /var/log/apache/
EXPOSE 80
CMD ["httpd-foreground"]
