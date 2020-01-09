FROM ubuntu:latest
RUN apt-get update && apt-get install -y apache2 git
RUN cd /var/www/html/ && rm *
RUN git clone https://github.com/mxkmp29/HelloWorld.git /var/www/html/
CMD /usr/sbin/apache2ctl -D FOREGROUND
