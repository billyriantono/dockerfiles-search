###########################
#Version 1, 27/08/2019
#Proxy another docker container to nginx x exposed, using YML
##########################
FROM nginx
##
RUN rm /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf
CMD service nginx start
####
