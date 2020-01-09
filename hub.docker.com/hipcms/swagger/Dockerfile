FROM swaggerapi/swagger-ui:latest

# copy the modified index.html (and jQuery) into the image
COPY index.html /usr/share/nginx/html/index.html
COPY jquery-3.2.0.min.js /usr/share/nginx/html/jquery-3.2.0.min.js

EXPOSE 8080

CMD [ "sh", "/usr/share/nginx/docker-run.sh" ]
