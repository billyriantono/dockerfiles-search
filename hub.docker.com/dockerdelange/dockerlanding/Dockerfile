###########################
#Cornel edit this 19 Dec 2017
#Creating a Container, where NGINX
#serves up static files and some images
#from forlder populated by this dockerfile
#I should use a volume, mainly just testing NGINX config
##########################
FROM nginx
COPY . /usr/share/nginx/html
##
#Added this for static image
RUN rm /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx

RUN mkdir -p /var/data/images
#WORKDIR /var/data/images
COPY dockerhero.jpg /var/data/images
COPY docker.html /var/data/images
#Now for the HTML files
RUN mkdir -p /var/www/html
#WORKDIR /var/www/html
COPY index.html /var/www/html
COPY dockerhero.jpg /var/www/html

EXPOSE 668
CMD service nginx start
#END of adding stuff for static images
##
