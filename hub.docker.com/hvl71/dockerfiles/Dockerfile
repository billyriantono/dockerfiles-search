FROM ubuntu
RUN apt-get update; apt-get install -y nginx
RUN echo 'hi, I am in your nice little container' >/var/www/html/index.html
EXPOSE 80
CMD ["/usr/sbin/nginx","-g","daemon off;"]
#add metadata which can be seen by "docker inspect". Place all in one line in order to avoid generating an image layer per instruction
LABEL location="Copenhagen" type="Sandbox" os="ubuntu" author="HVL71"
