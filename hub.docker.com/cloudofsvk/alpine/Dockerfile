FROM alpine:latest
MAINTAINER SVK
RUN apk update && apk add apache2 bash && \
rm -rf /var/cache/apk/* && \
mkdir -p /run/apache2 
ADD ./index.html /var/www/localhost/htdocs/ 
ADD ./svk.cgi /var/www/localhost/cgi-bin/
RUN chmod +x /var/www/localhost/cgi-bin/svk.cgi && \
sed -i "s-#LoadModule cgi_module-LoadModule cgi_module-g" /etc/apache2/httpd.conf && \
apk add tzdata && \
cp /usr/share/zoneinfo/Asia/Kolkata /etc/localtime && \
echo "Asia/Kolkata" > /etc/timezone && \
apk del tzdata
EXPOSE 80
ENTRYPOINT ["httpd", "-D", "FOREGROUND"]
