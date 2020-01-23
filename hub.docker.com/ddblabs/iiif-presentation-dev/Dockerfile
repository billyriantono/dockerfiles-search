FROM library/httpd:alpine
MAINTAINER Michael Büchner <m.buechner@dnb.de>

RUN apk add sed
RUN rm /usr/local/apache2/htdocs/index.html
COPY htdocs/ /usr/local/apache2/htdocs/
RUN find /usr/local/apache2/htdocs/ -type f -name "*.json" -exec sed -i 's/{{IIIF_IMAGE_SERVER}}/https:\/\/iiif-image-dev.cfapps.eu10.hana.ondemand.com\/iiif\/2/g' {} \;

EXPOSE 80
