FROM nginx

RUN apt-get -y update
RUN apt-get install -y dos2unix

COPY /App /usr/share/nginx/html/vocbench
COPY /Nginx/nginx.conf /etc/nginx/nginx.conf
#COPY /entrypoint.sh /

RUN dos2unix /etc/nginx/nginx.conf
#RUN dos2unix /entrypoint.sh

#EXPOSE 80

#ENTRYPOINT ["/entrypoint.sh"]