# ok.. then we play with linux containers instead..

#I switch to linux containers and run: 
#docker run --detach --publish 80:80 --name webserver nginx

#then I can browse a nginx site on http://localhost cool!!

#docker pull hvl71/docker-site:release-master
#docker run --detach --publish 80:80 --name web hvl71/docker-site:release-master
#open http://localhost/page2.htm

FROM nginx
COPY static-html-directory /usr/share/nginx/html