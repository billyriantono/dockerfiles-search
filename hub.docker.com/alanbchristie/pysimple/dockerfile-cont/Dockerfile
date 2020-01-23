FROM nginx:1.9.14

COPY geoknow.eu.tar.gz /tmp/
RUN tar -xvzf /tmp/geoknow.eu.tar.gz -C /tmp/
RUN cp -R /tmp/geoknow.eu/* /usr/share/nginx/html/
