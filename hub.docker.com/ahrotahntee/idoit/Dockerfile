FROM ahrotahntee/nginx-php7:latest
RUN apk --no-cache add php7-mysqli php7-pdo php7-pdo_mysql php7-xml php7-session php7-gd php7-simplexml php7-mcrypt php7-curl php7-json
WORKDIR /srv
ADD php.ini /etc/php7/php.ini
ADD idoit-open-1.13.zip /srv
RUN unzip idoit-open-1.13.zip && rm idoit-open-1.13.zip
RUN chmod 777 -R /srv/upload
