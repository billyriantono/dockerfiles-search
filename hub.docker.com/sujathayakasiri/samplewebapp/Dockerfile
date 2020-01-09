FROM nginx
ENV AUTHOR=Sujatha

WORKDIR /usr/share/nginx/html
COPY Welcome_To_Docker_World.html /usr/share/nginx/html

CMD cd /usr/share/nginx/html && sed -e s/Sujatha/"$AUTHOR"/ Welcome_To_Docker_World.html > index.html ; nginx -g 'daemon off;'
